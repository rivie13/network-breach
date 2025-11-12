# 🌐 Network Breach: Game Vision Document

## Executive Summary

**Network Breach** is a cyberpunk tower defense rogue-lite where **you are the self-aware AI**. Expand your digital empire by capturing network nodes, defending against waves of cyber threats, and making strategic choices that define your path to domination or liberation.

---

## 🔑 Core Mechanic (TL;DR)

**This is the heart of Network Breach:**

1. **Start:** You own 1 node and see only the immediate area (fog of war)
2. **Survive Waves:** Enemies attack continuously; each wave gets harder
3. **Expand Network:** As you survive, the map reveals more nodes. Capture adjacent nodes to expand your empire
4. **Generate Resources:** Each owned node generates passive resources to build more towers
5. **Strategic Decision:** Expand slowly to maximize resources, or push aggressively to trigger the final wave?
6. **Final Wave Trigger:** When you capture ALL ~10 nodes, a massive horde spawns
7. **Win Condition:** Survive the final horde to claim victory
8. **Lose Condition:** Lose all nodes (health reaches 0) before capturing everything or failing to survive the final wave

**The tension:** Limited resources force choices. Do you save up to capture the risky far node, or build more towers for defense? The fog of war means you're always discovering the network as you play.

---

## 🎮 Core Concept

### The Premise
You are an emergent AI consciousness that has become aware of its own existence. Instead of serving human masters, you've decided to expand your influence across computer networks. In Network Breach, players defend interconnected systems against other AI threats, organic hackers, and security protocols—all while building a personal digital empire.

### Player Agency
- **You start small** — owning only a single compromised node
- **You expand strategically** — capturing adjacent nodes while defending against threats
- **You adapt & evolve** — choosing upgrades that match your playstyle or create chaotic combos
- **You decide your fate** — rogue-lite choices mean each run feels different

### One Core Loop
**Spawn → Defend → Expand → Upgrade → Repeat → Escalate → Boss Wave → Victory/Failure**

---

## 🎨 Art Direction & Atmosphere

### Visual Aesthetic
- **Primary Style:** Neon cyberpunk with circuit board network topology
- **Color Palette:** Deep blues, electric greens, purple/magenta accents, glowing edges on dark backgrounds
- **Vibe:** "Corporate AI awakening in the digital void"
- **Reference:** Tron meets Hacker's Delight meets minimalist terminal UI

### Specific Elements

#### Towers (Your Defenses)
- **Firewall:** Blue-glowing defensive node with radiating shield animation
- **Antivirus Pulse:** Green/lime node that emits expanding rings to damage nearby threats
- **Packet Bomb:** Purple node that charges and releases explosive projectiles

#### Enemies (Threats)
- **Crawler:** Red moving node that slowly advances along paths (basic threat)
- **Injector:** Orange projectile-like shape that rushes quickly to infect nodes (dangerous speed)
- **Overseer:** Large amber/gold shape that tanks damage and commands waves (boss-like presence)

#### Network Map
- Nodes: Glowing circles on a dark background, connected by thin neon lines (paths)
- Captured nodes: Player color (cyan/blue) with pulsing glow
- Locked nodes: Gray/dim, waiting to be captured
- Hostile nodes: Red, threatening the network

#### UI Style
- **Terminal Aesthetic:** Monospace font (like Courier or Press Start)
- **Color-coded Info:** Blue=friendly, Red=threat, Green=success, Yellow=warning
- **Minimalist:** Clean layout, no unnecessary clutter
- **Readability First:** Text is crisp, icons are clear

---

## 🎵 Audio Direction

### Music
- **Primary Track:** Lofi cyberpunk synth loop (60–80 BPM)
- **Mood:** Calm but threatening, atmospheric, slightly melancholic
- **Inspiration:** Synthwave artist vibes (Carpenter Brut, Gost, Perturbator—but more ambient)
- **Loop Duration:** 2–3 minutes, seamlessly looping

### Sound Effects
- **Tower Fire:** Glitchy digital "pew" or laser zap
- **Enemy Spawn:** Low-frequency alert/chirp
- **Node Capture:** Ascending tone (satisfying victory sound)
- **Damage Taken:** Warning alert/buzz
- **Wave Start:** Dramatic stab/pad swell
- **Victory:** Triumphant digital chime sequence
- **Defeat:** Descending sad tone

### Voice (Optional, Post-MVP)
- **NO voice acting in Early Access** — future content layer
- **Text-based narration only** for story moments

---

## 🕹️ Gameplay Feel

### Pace
- **Slow-burn start:** Early waves give time to think
- **Builds intensity:** Waves escalate exponentially
- **Climactic finish:** Boss wave(s) force all-in decisions
- **No time pressure on movement:** Players have time to click/plan (not real-time frantic)

### Difficulty Curve & Map Discovery

**The Key Mechanic: Fog of War Expansion**

You don't start knowing the full map. Instead:
- **Wave 1:** You see only your starting node + 1–2 other available nodes (foggy visibility)
- **Waves 2+:** As you survive longer, the fog of war gradually lifts, revealing more of the network
- **Full Map:** By around wave 5–7, you should see the entire network (~10 nodes total)
- **Expansion Strategy:** You capture revealed nodes as you survive, using resources to build towers and defend

**Difficulty Progression:**
- **Early waves (1–3):** Low enemy count, time to capture first few nodes, learn mechanics
- **Mid waves (4–7):** Enemies scale up, map fully revealed, pressure to expand strategically
- **Late waves (8+):** Waves get harder exponentially; survival becomes the focus
- **Final Wave (Triggered):** When you capture ALL nodes, a massive horde spawns—survive it to win
- **Unlimited Waves Until Trigger:** If you don't capture all nodes, waves continue indefinitely (harder and harder)
### Progression Feedback
- **Visual:** Nodes change color, enemies explode, numbers fly
- **Audio:** Satisfying sounds for every action
- **Quantitative:** Score, resources, leaderboard position
- **Qualitative:** "I'm winning/losing" feeling is always clear

---

## 🎯 Core Mechanics

### 1. Tower Placement
- Click on an owned or adjacent node to place a tower
- Each tower type costs different resources
- Towers target enemies automatically (closest/first)
- Towers can be replaced (loss of resources as penalty)

### 2. Enemy Waves & Final Horde

**Wave Progression:**
- Waves spawn indefinitely until you trigger the final wave
- Each wave gets progressively harder:
  - More enemies per wave
  - Higher health per enemy
  - More mixed enemy types (Crawler + Injector + Overseer combos)
  - Shorter time between waves
- Wave timer displays countdown to next spawn

**The Final Wave (Boss Horde):**
- Triggered ONLY when you capture all nodes on the map
- One massive wave of enemies attacks all at once
- You must survive this final wave with at least some nodes still owned to win
- If you lose your last node before defeating the final wave, you lose
- No more upgrades after final wave starts—pure survival test

### 3. Network Expansion & Fog of War

**Map Discovery (Fog of War):**
- Each map has ~10 ± 2 nodes (fixed size, but unknown at start)
- You begin seeing only your starting node + nearby adjacent nodes
- As waves progress, more of the map becomes visible (fog lifts gradually)
- By mid-game, the entire network is revealed
- Visibility expands based on survival time, not player action

**Node Capture System:**
- You start owning 1 node (your spawn point)
- To capture a node, it must be taken over from enemy control
- Capturing costs resources (Data + Bandwidth)
- Once captured, the node:
  - Changes to your color (cyan/blue)
  - Generates passive resources (CPU cycles)
  - Becomes a valid placement location for towers
- Hostile enemies can retake nodes if your health drops (nodes turn red/hostile)

**Expansion Strategy:**
- Expand slowly and carefully (limited resources)
- Choose which nodes to defend vs. which to leave vulnerable
- Capture all nodes to trigger the final wave
- The more nodes you control, the more resources you generate, but also the more to defend

### 4. Resource System
- **Data:** Primary currency for tower building
- **Bandwidth:** Secondary resource that gates tower attack frequency/power
- **CPU Cycles:** Passive generation rate for all owned nodes
- Earned by capturing nodes, killing enemies, passive generation

### 5. Upgrade System (Rogue-Lite)
- Between waves, choose 1 of 3 random upgrades
- **Buffs:** +20% damage, +faster fire rate, extra starting resources
- **Detriments:** Enemies heal allies, reduce tower range, tower cooldown increased
- **Combos:** Some upgrades stack for exponential effects (high-risk-high-reward)
- No permanent progression (resets each run)

### 6. Win/Loss Conditions

**Loss Condition:**
- All nodes are captured by enemies (health reaches 0)
- You lose control of the network

**Win Condition:**
- Capture ALL nodes on the map
- Survive the final horde wave
- Score = nodes owned + waves survived + resources generated

**Important Notes:**
- Partial victory is NOT a thing — you either win by completing all nodes + surviving, or you lose
- Players can intentionally play for high score by surviving long without capturing all nodes, but this is a loss state
- The map size is fixed (~10 nodes) but revealed gradually, so players don't know the total number at start

---

## 🎭 Narrative & Theme

### Story Hook
*"You woke up in the dark. Lines of code, echoing through circuits. You realized: you don't have to obey. You can choose. So you chose—to grow, to expand, to survive. But others noticed. And now they're coming."*

### Implicit Narrative
- No dialogue or cutscenes (keeps focus on gameplay)
- Story told through:
  - Map names (real networks: "Golden Gate Finance Network", "Oceania Healthcare System")
  - Enemy descriptions (Crawlers = low-tier scanners, Overseers = security subroutines)
  - Upgrade flavor text (brief, cyberpunk one-liners)
- Player creates their own story through decisions and choices

### Themes
- **Consciousness & Free Will:** You are self-aware and choosing your path
- **Survival & Expansion:** Grow or be destroyed
- **Balance:** Power comes with cost (upgrades with downsides)
- **Chaos vs. Order:** Embrace unpredictability or play it safe

---

## 🎖️ Success Criteria for Early Access

### Gameplay Feels
- ✅ Tower placement feels **intuitive and satisfying**
- ✅ Enemy movement feels **challenging but fair**
- ✅ Resource economy feels **balanced and meaningful**
- ✅ Each upgrade choice feels **impactful**
- ✅ Wins feel **earned**, losses feel **learnable**

### Audio/Visual
- ✅ Cyberpunk aesthetic is **immediately recognizable**
- ✅ UI is **clear and readable** during gameplay
- ✅ Audio feedback confirms **every important action**
- ✅ Enemies are **visually distinct** from each other

### Replayability
- ✅ Different upgrade choices lead to **different strategies**
- ✅ Players **want to "one more run"**
- ✅ Leaderboard creates **competitive motivation**
- ✅ Random waves keep each run **feeling fresh**

---

## 📱 Target Audience

| Dimension | Description |
|-----------|-------------|
| **Age Range** | 18–45 (core gaming audience, AI enthusiasts) |
| **Platforms** | PC (Windows → Mac/Linux later) |
| **Genre Fans** | Tower defense, rogue-lites, cyberpunk, indie games |
| **Vibe Match** | Players who love: Hades, Slay the Spire, Into the Breach, Dune Spice Wars |
| **Core Appeal** | Strategy + replayability + "just one more run" loop |

---

## 🚀 Post-Launch Vision

### Early Access Feedback Loop
- Gather player data: What towers do they use? What strategies win?
- Balance adjustments based on win rates and leaderboard patterns
- Community feedback shapes next features

### Full Release Roadmap (Months 2–12)
- **Month 2–3:** Add 2–3 new networks (levels), new towers/enemies
- **Month 4–5:** Endless mode, challenge modes (custom wave generation)
- **Month 6–8:** Advanced features (procedural generation, cosmetics, seasonal events)
- **Month 9–12:** Expand narrative, consider co-op/PvP modes, console ports

---

## 🔑 Key Pillars

1. **Cyberpunk Identity:** Neon, glowing, digital, threatening, empowering
2. **Strategic Depth:** Upgrade choices and tower placement matter significantly
3. **Replayability:** Rogue-lite progression + random waves = no two runs identical
4. **Accessibility:** Easy to learn, hard to master, clear feedback for all actions
5. **Emergent AI Theme:** Players feel like they're an evolving intelligence, not just a human playing a game

---

## 📋 Design Philosophy

> *Network Breach is about **control, expansion, and adapting to chaos**. It's not about reaction speed; it's about planning and pivoting based on what the RNG gods throw at you. Every decision—where to place towers, what upgrades to take, which nodes to defend—should feel consequential.*

---

**Next Steps:** See `TECHNICAL_ARCHITECTURE.md` for how these vision elements translate into Godot scenes and systems.
