# 🎮 Network Breach: Core Mechanic Explained

This document provides an in-depth explanation of how the fog-of-war map discovery, node capture, and final wave system work together to create the core gameplay loop.

---

## The Three Core Systems

### 1. Fog of War (Map Discovery)

#### What is Fog of War?
The player doesn't see the entire map at game start. Instead, they see a "foggy" version that gradually clears as they survive longer.

#### How It Works

**Visual Representation:**
- **Visible nodes:** Shown in full color/detail, can be captured/built on
- **Hidden nodes:** Shown as gray/dim question marks or invisible entirely
- **Paths between nodes:** Only shown for visible nodes

**Discovery Timeline:**
```
Wave 1:    ████░░░░░░  (Player sees ~2-3 nodes)
Wave 2-3:  ██████░░░░  (Player sees ~5 nodes)
Wave 4-5:  ████████░░  (Player sees ~8 nodes)
Wave 6+:   ██████████  (Player sees entire ~10 node network)
```

**Technical Implementation:**
- The full map (all ~10 nodes) exists in the scene from start
- Nodes are hidden by default (disabled, invisible, greyed out)
- Based on `waves_survived`, reveal new nodes progressively
- Recommendation: Reveal ~1-2 new nodes per wave

**Example Code Logic:**
```gdscript
# In NetworkMap or Node Manager
func reveal_nodes_for_wave(wave_number):
    var nodes_to_reveal = 1 + (wave_number % 3)  # Roughly 1-2 per wave
    
    # Reveal nodes adjacent to already-visible nodes
    for revealed_node in visible_nodes:
        for adjacent in revealed_node.get_adjacent_nodes():
            if not adjacent.is_visible and nodes_to_reveal > 0:
                adjacent.reveal()
                nodes_to_reveal -= 1
```

#### Design Rationale
- **Pacing:** Players aren't overwhelmed at start; map grows with their understanding
- **Strategic Depth:** "Should I expand toward the revealed edge, or save resources?"
- **Replayability:** Different reveal patterns = different games
- **Tension:** "What if there's a node I can't reach?"

---

### 2. Node Capture System

#### What Nodes Are
Nodes are the discrete territories of the network map. Each node is:
- A physical location on the map
- A resource generator (if owned)
- A tower placement location (if owned)
- A target for enemies (all enemy waves attack nodes)

#### Node States

```
STATE              COLOR    PLAYER CAN...              PLAYERS CAN...
═══════════════════════════════════════════════════════════════════════
Owned              Cyan     Build towers, capture     Defend, expand
                   (Blue)   adjacent nodes            

Neutral/Visible    Gray     Attempt to capture       Attack/defend if
                            (pay resources)          tower is built

Hidden             None     Cannot interact (yet)    Not visible

Hostile            Red      None (until recapture)   Attacked by this
                                                      node's enemies
```

#### Capture Mechanics

**Pre-Capture:**
- Node must be available and connected to a node you already own
- Capturing costs: X Data + Y Bandwidth (varies by game balance)
- Capture is instant (happens when you pay the cost and click)

**Post-Capture:**
- Node changes to your color (cyan/blue)
- Immediately starts generating passive resources
- Now available for tower placement
- Connected to your resource network

**Example Data:**
```
Capture Cost:
- Data: 25
- Bandwidth: 10

Resource Generation Per Wave (once owned):
- CPU Cycles: +5 per wave
- Data: +2 per wave
- Bandwidth: +1 per wave
```

#### Why This Matters
- **Limited Resources:** You can't capture all nodes at once; forces strategic prioritization
- **Expansion vs. Defense:** Do you capture the far node or build more towers locally?
- **Network Topology:** The map layout directly impacts strategy (bottleneck nodes are valuable)
- **Progressive Complexity:** Early waves let you capture cheaply; later waves you need more resources

---

### 3. The Final Wave System

#### What Triggers the Final Wave?

**Condition:** Player owns ALL nodes on the map (100% captured)

**What Happens:**
1. After the wave where you capture the last node completes
2. Next wave is announced as "FINAL WAVE" or "HORDE INCOMING"
3. A massive number of enemies spawn at once
4. Player gets ONE upgrade choice (optional)
5. Waves stop after this—only the horde attacks

#### The Final Wave Specifics

**Enemy Count:**
- Normal wave 10: ~25 enemies
- Final wave: ~50-75 enemies (massive horde)

**Enemy Types:**
- Mix of all three types (Crawler, Injector, Overseer)
- Emphasis on Overseer (tank enemies) to pressure defenses
- Example: 60 Crawlers + 10 Injectors + 5 Overseers

**Victory Condition:**
- Survive until all horde enemies are defeated
- Must maintain at least 1 node under your control
- If you lose your last node, you lose immediately

#### Example Timeline

```
Waves 1-9:   Gradual difficulty increase, normal waves
Wave 9 End:  Player captures final (10th) node
             Map shows 100% owned

Wave 10:     FINAL WAVE ANNOUNCED
             Massive horde spawns
             
             Player defends desperately
             
             Horde wiped out
             
             VICTORY! Score calculated and sent to leaderboard
```

#### Design Rationale
- **Clear Win State:** Players know exactly what they're working toward
- **Climax:** Everything builds to this one intense moment
- **Replayability:** Players can try different expansion strategies to reach this moment different ways
- **Leaderboard Worthy:** "I beat the horde on wave 14 with 9 nodes captured!"

---

## The Game Loop

### A Single Run's Flow

```
GAME START
   ↓
[Wave 1] Spawn ~2-3 enemies
   ├─ Defend your starting node
   ├─ See ~2-3 nodes on map (fog of war)
   ├─ Earn first resources
   └─ → Wave completes → Upgrade choice (pick 1 of 3)
   
[Waves 2-3] Spawn ~5-10 enemies
   ├─ Map expands (reveal more nodes)
   ├─ Build more towers
   ├─ Decide: capture first adjacent node?
   ├─ Passive resources grow
   └─ → After each wave → Upgrade choice
   
[Waves 4-6] Spawn ~15-25 enemies
   ├─ Full map now revealed
   ├─ Multiple nodes now captured
   ├─ Strategic: defend existing or capture new?
   ├─ Resource pressure increases
   ├─ Waves get harder (more Injectors/Overseers)
   └─ → After each wave → Upgrade choice
   
[Waves 7-9] Spawn ~25-40 enemies
   ├─ Decision: do we go for the win?
   ├─ Plan final expansion
   ├─ Capture remaining nodes
   ├─ Focus on defense of critical nodes
   ├─ If we own <5 nodes: wave difficulty is punishing
   └─ → After each wave → Upgrade choice
   
[Wave 10] FINAL WAVE - MASSIVE HORDE (~50-75 enemies)
   ├─ All nodes are yours
   ├─ Make final upgrade choice
   ├─ Waves stop appearing
   ├─ PURE SURVIVAL MODE
   ├─ If you lose any node: DEFEAT (instant lose)
   ├─ If you kill all enemies: VICTORY
   └─ → Game ends → Score to leaderboard
```

### Key Moments in a Run

**Moment 1: First Expansion (Wave 2-3)**
- Player sees the map expanding
- Decision: "Should I capture this node?"
- First real strategic choice

**Moment 2: Mid-Game Crunch (Wave 5-7)**
- Map fully revealed
- Resources stretched thin
- "Can I afford to capture the next node?"

**Moment 3: The Push (Wave 8-9)**
- Decide: go for the win by capturing all nodes?
- Or play defensively and maximize score?
- Last few nodes are the most expensive (strategy)

**Moment 4: The Final Wave**
- All nodes captured
- Horde incoming
- "Can I survive this?"

---

## Map Design Implications

### Map Size
- **Standard:** ~10 nodes (8-12 acceptable)
- **Why:** Feels large enough to be a challenge, small enough to complete in one run
- **Layout:** Connected in a graph (some bottlenecks, some open areas)

### Node Adjacency
- Each node connects to 1-4 adjacent nodes
- No isolated nodes (reachable from start)
- Some nodes are "dead ends" (only one connection)
- Some nodes are "hubs" (3+ connections) — valuable to control

### Example Map Layout
```
     [A]---[B]---[C]
      |     |      |
     [D]--[E]     [F]
           |       |
          [G]-----[H]
           |
          [I]
           |
          [J]
```

**Properties:**
- Start at A (position 1)
- 10 nodes total
- Hub nodes: B (3 connections), E (4 connections)
- Dead-ends: A, F, J, C (bottlenecks)
- Average path to farthest node: 4-5 captures

---

## Balance Tuning Questions

### For You During Development

1. **Fog of War Speed:** How fast should the map reveal?
   - Too fast: Player sees everything, no surprise
   - Too slow: Player frustrated they can't plan
   - Sweet spot: Reveal complete map by wave 5-6

2. **Capture Cost:** How much should capturing cost?
   - Too expensive: Player can't expand, trapped
   - Too cheap: Player expands too easily, no challenge
   - Sweet spot: Forces meaningful decisions each wave

3. **Final Wave Difficulty:** How many enemies in the horde?
   - Too few: Final wave is a joke (anti-climactic)
   - Too many: Final wave is impossible (frustrating)
   - Sweet spot: Winnable with good tower placement, challenging with bad

4. **Node Resource Generation:** How much do owned nodes produce?
   - Too much: Player can expand infinitely
   - Too little: Player always broke
   - Sweet spot: Forces choices between expanding and defending

---

## Critical Implementation Details

### The Fog of War Algorithm

**Recommendation: "Radial Discovery"**
```gdscript
# Calculate visibility based on wave count
var visibility_radius = 1 + (current_wave / 3)  # Grows ~1 every 3 waves

# For each owned node, reveal nodes within the radius
for owned_node in player_owned_nodes:
    for visible_node in get_nodes_within_radius(owned_node, visibility_radius):
        visible_node.reveal()
```

**Result:** Player's visible area expands outward from their owned nodes like ripples

### Node State Tracking

**Each Node Needs:**
```gdscript
class NetworkNode:
    var owner: String  # "player", "enemy", "neutral"
    var is_visible: bool
    var is_captured: bool
    
    var health: int
    var max_health: int
    
    var towers: Array[Tower]
    
    func capture_by_player():
        owner = "player"
        is_captured = true
        start_resource_generation()
    
    func retaken_by_enemy():
        owner = "enemy"
        is_captured = false
        stop_resource_generation()
```

### Win Condition Check

```gdscript
func check_win_condition():
    if current_wave_is_final and all_enemies_dead:
        player_owned_nodes = count_player_nodes()
        if player_owned_nodes >= total_nodes:
            trigger_victory()
    
    if player_owned_nodes == 0:
        trigger_defeat("All nodes lost")
```

---

## Communication to Player

### What the Player Should Always Know

1. **Current Status:**
   - "You own X of Y nodes"
   - "Horde incoming when all nodes captured"

2. **Map State:**
   - Visible vs. hidden nodes must be visually distinct
   - Path to new nodes should be clear

3. **Fog of War Progress:**
   - Optional: "3 more waves until next area revealed"
   - Visual: Nodes fade from gray to color as they're revealed

4. **Final Wave Warning:**
   - Big announcement: "FINAL WAVE INCOMING"
   - Clear explanation: "Survive the horde to win!"

### UI Messages

```
[Wave 1] "You own 1 of 3 visible nodes"
[Wave 4] "Map expanding... 7 of 10 nodes discovered"
[Wave 7] "You own 8 of 10 nodes. Two more to go!"
[Wave 9] "LAST NODE CAPTURED!"
[Wave 10] "⚠️ FINAL WAVE INCOMING - MASSIVE HORDE DETECTED ⚠️"
[Final]   "ALL ENEMIES DEFEATED - VICTORY!"
```

---

## Summary for Development

**Week 1 MVP (Ignore Fog of War):**
- All nodes visible from start
- Can capture adjacent nodes
- Basic win condition: capture all nodes + survive horde

**Week 2 (Add Fog of War):**
- Hide nodes at start
- Progressively reveal as waves progress
- UI message about fog of war expansion

**Week 3 (Polish):**
- Tune costs, enemy counts, discovery speed
- Add announcements
- Balance based on playtesting

---

**Remember:** The fog of war + node capture + final wave creates a clear progression arc. Players always know what they're working toward, and the map constantly evolves beneath them.
