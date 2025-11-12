# 🏗️ Network Breach: Technical Architecture Document

## Project Overview

**Engine:** Godot 4.5.1  
**Platform (MVP):** Windows PC  
**Resolution:** 1920x1080 (target), scales down gracefully  
**Build Target:** Steam Early Access  

---

## 📂 Folder Structure

```
network-breach/
├── project.godot                 # Project configuration
├── README.md                     # Project readme
├── GAME_VISION.md               # Design doc (what/why)
├── TECHNICAL_ARCHITECTURE.md    # This file (how/where)
├── ONE_MONTH_MILESTONE.md       # Release timeline (when)
├── WEEK_1_TASK_BREAKDOWN.md     # Task list (what to do)
│
├── addons/                      # Third-party plugins
│   └── godot-steam/             # GodotSteam plugin (added Week 3)
│
├── assets/                      # All raw/imported content
│   ├── sprites/
│   │   ├── towers/
│   │   │   ├── firewall.png
│   │   │   ├── antivirus.png
│   │   │   └── packet_bomb.png
│   │   ├── enemies/
│   │   │   ├── crawler.png
│   │   │   ├── injector.png
│   │   │   └── overseer.png
│   │   ├── nodes/
│   │   │   ├── node_locked.png
│   │   │   ├── node_player.png
│   │   │   └── node_hostile.png
│   │   ├── ui/
│   │   │   ├── button_normal.png
│   │   │   ├── button_hover.png
│   │   │   └── ui_icons.png
│   │   └── fx/
│   │       ├── impact.png
│   │       ├── explosion.png
│   │       └── capture_effect.png
│   │
│   ├── sounds/
│   │   ├── sfx/
│   │   │   ├── tower_fire.wav
│   │   │   ├── enemy_spawn.wav
│   │   │   ├── node_capture.wav
│   │   │   ├── damage.wav
│   │   │   ├── wave_start.wav
│   │   │   ├── victory.wav
│   │   │   └── defeat.wav
│   │   └── music/
│   │       └── cyberpunk_loop.wav
│   │
│   ├── fonts/
│   │   └── courier_terminal.ttf
│   │
│   └── data/
│       ├── tower_stats.json
│       ├── enemy_stats.json
│       └── upgrade_database.json
│
├── scenes/                      # Game scenes (organized by function)
│   ├── game/
│   │   ├── main.tscn            # Root game scene
│   │   ├── main.gd
│   │   │
│   │   ├── world.tscn           # Game world container
│   │   ├── world.gd
│   │   │
│   │   ├── map/
│   │   │   ├── network_map.tscn # TileMap + navigation mesh
│   │   │   ├── network_map.gd
│   │   │   └── network_paths.tres # Navigation polygon resource
│   │   │
│   │   ├── towers/
│   │   │   ├── tower_base.tscn  # Base tower prefab
│   │   │   ├── tower_base.gd
│   │   │   ├── firewall.tscn
│   │   │   ├── firewall.gd
│   │   │   ├── antivirus.tscn
│   │   │   ├── antivirus.gd
│   │   │   ├── packet_bomb.tscn
│   │   │   └── packet_bomb.gd
│   │   │
│   │   ├── enemies/
│   │   │   ├── enemy_base.tscn  # Base enemy prefab
│   │   │   ├── enemy_base.gd
│   │   │   ├── crawler.tscn
│   │   │   ├── crawler.gd
│   │   │   ├── injector.tscn
│   │   │   ├── injector.gd
│   │   │   ├── overseer.tscn
│   │   │   └── overseer.gd
│   │   │
│   │   ├── nodes/
│   │   │   ├── network_node.tscn # Capturable node prefab
│   │   │   └── network_node.gd
│   │   │
│   │   ├── effects/
│   │   │   ├── impact_effect.tscn
│   │   │   ├── explosion_effect.tscn
│   │   │   └── capture_effect.tscn
│   │   │
│   │   └── waves/
│   │       ├── wave_manager.tscn
│   │       └── wave_manager.gd
│   │
│   ├── ui/
│   │   ├── hud.tscn             # In-game UI overlay
│   │   ├── hud.gd
│   │   ├── health_display.tscn
│   │   ├── health_display.gd
│   │   ├── resource_display.tscn
│   │   ├── resource_display.gd
│   │   ├── wave_timer.tscn
│   │   ├── wave_timer.gd
│   │   ├── upgrade_panel.tscn   # Between-wave upgrade UI
│   │   ├── upgrade_panel.gd
│   │   ├── game_over_screen.tscn
│   │   ├── game_over_screen.gd
│   │   ├── pause_menu.tscn
│   │   └── pause_menu.gd
│   │
│   ├── menus/
│   │   ├── main_menu.tscn       # Main menu (Week 3)
│   │   ├── main_menu.gd
│   │   ├── settings_menu.tscn
│   │   └── settings_menu.gd
│   │
│   └── screens/
│       ├── splash_screen.tscn   # Game studio splash
│       └── loading_screen.tscn  # Loading indicator
│
├── scripts/                     # Core game logic
│   ├── managers/
│   │   ├── game_state_manager.gd      # Global game state
│   │   ├── resource_manager.gd        # Resource economy
│   │   ├── upgrade_system.gd          # Upgrade logic
│   │   ├── leaderboard_manager.gd     # Steam integration (Week 3)
│   │   └── audio_manager.gd           # Sound/music
│   │
│   ├── systems/
│   │   ├── tower_system.gd      # Tower placement/management
│   │   ├── enemy_system.gd      # Enemy spawning/despawning
│   │   ├── pathfinding.gd       # Navigation setup
│   │   └── input_system.gd      # Player input handling
│   │
│   ├── components/
│   │   ├── health_component.gd  # Health tracking mixin
│   │   ├── damage_component.gd  # Damage calculation mixin
│   │   ├── movement_component.gd # Movement logic mixin
│   │   └── targeting_component.gd # Targeting logic mixin
│   │
│   ├── data/
│   │   ├── tower_data.gd        # Tower stats/definitions
│   │   ├── enemy_data.gd        # Enemy stats/definitions
│   │   ├── upgrade_data.gd      # Upgrade pool/definitions
│   │   └── resource_data.gd     # Resource type definitions
│   │
│   └── events/
│       └── event_bus.gd         # Signal hub for all events
│
└── exports/                     # Build outputs (generated)
    └── windows/
```

---

## 🎬 Scene Hierarchy (Runtime)

### Main Game Flow Structure

```
Main (main.tscn - root)
│
├── World (Node2D)
│   ├── NetworkMap (TileMapLayer)
│   │   ├── Base terrain tiles
│   │   └── NavigationRegion2D (pathfinding mesh)
│   │
│   ├── NetworkNodes Container (Node2D)
│   │   ├── NetworkNode (captured node 1)
│   │   ├── NetworkNode (captured node 2)
│   │   └── NetworkNode (locked node 3)
│   │
│   ├── TowerContainer (Node2D)
│   │   ├── Tower (Firewall) - targeting enemies
│   │   ├── Tower (Antivirus) - emitting pulses
│   │   └── Tower (PacketBomb) - charging blast
│   │
│   ├── EnemyContainer (Node2D)
│   │   ├── Enemy (Crawler) - moving along path
│   │   ├── Enemy (Injector) - rushing forward
│   │   └── Enemy (Overseer) - slow tank
│   │
│   ├── EffectsLayer (CanvasLayer)
│   │   ├── Impact particles
│   │   └── Capture animations
│   │
│   └── WaveManager (Node)
│       └── Handles spawning logic
│
├── GUI (Control - UI Layer)
│   ├── HUD (Control)
│   │   ├── ResourceDisplay (Label/HBox)
│   │   ├── HealthDisplay (ProgressBar)
│   │   ├── WaveTimer (Label)
│   │   └── GameLog (RichTextLabel) - event messages
│   │
│   ├── UpgradePanel (Control) - hidden until between waves
│   │   ├── UpgradeChoice1 (Button)
│   │   ├── UpgradeChoice2 (Button)
│   │   └── UpgradeChoice3 (Button)
│   │
│   ├── GameOverScreen (Control) - hidden until win/loss
│   │   ├── Result title (Label)
│   │   ├── Stats display (VBox)
│   │   └── Restart/Menu buttons
│   │
│   └── PauseMenu (Control) - hidden until paused
│       ├── Resume button
│       ├── Settings button
│       └── Quit button
│
└── Autoload Managers (GlobalScope - visible from anywhere)
    ├── EventBus (signal hub)
    ├── GameStateManager (persistent data)
    ├── ResourceManager (currency/resources)
    ├── AudioManager (sound/music)
    └── LeaderboardManager (Steam sync - Week 3)
```

---

## 🔌 Autoload Managers (Singletons)

These are registered in Project Settings → Autoload and persist across scenes:

### EventBus (event_bus.gd)
**Purpose:** Central signal dispatcher for all game events  
**Signals:**
```gdscript
signal wave_started(wave_number)
signal wave_completed()
signal enemy_spawned(enemy)
signal enemy_died(enemy, killer)
signal tower_placed(tower, position)
signal tower_destroyed(tower)
signal node_captured(node)
signal health_changed(new_health)
signal resources_changed(data, bandwidth, cpu)
signal upgrade_offered(upgrade1, upgrade2, upgrade3)
signal upgrade_selected(upgrade)
signal game_over(victory: bool)
signal game_paused(paused: bool)
```

### GameStateManager (game_state_manager.gd)
**Purpose:** Tracks current game state (wave number, difficulty, run data)  
**Properties:**
```gdscript
var current_wave: int
var current_health: int
var captured_nodes: Array
var total_score: int
var upgrades_applied: Array
var game_running: bool
var game_paused: bool
```

### ResourceManager (resource_manager.gd)
**Purpose:** Manages currency and resource economy  
**Resources:** Data, Bandwidth, CPU  
**Methods:**
- `add_resource(type, amount)`
- `spend_resource(type, amount) -> bool`
- `get_resource(type) -> int`

### AudioManager (audio_manager.gd)
**Purpose:** Centralized audio playback (music, SFX)  
**Methods:**
- `play_sfx(sfx_name)`
- `play_music(track_name)`
- `stop_music()`

---

## 🎬 Core Scene Prefabs

### Enemy Base Prefab Structure
```
CharacterBody2D (enemy_base.gd)
├── Sprite2D (visual representation)
├── CollisionShape2D (physics body)
├── NavigationAgent2D (pathfinding)
├── Area2D (damage radius - optional)
│   └── CollisionShape2D
├── HealthComponent (health_component.gd - attached via script)
└── Timer (attack cooldown - if applicable)
```

**Base Script Responsibilities:**
- Initialize health, speed, damage values
- Handle pathfinding via NavigationAgent2D
- Detect collision with towers/nodes
- Emit signals on death
- Handle animation/visual state

### Tower Base Prefab Structure
```
Node2D (tower_base.gd)
├── Sprite2D (visual representation)
├── Area2D (attack range detector)
│   └── CollisionShape2D (circular range)
├── Marker2D (projectile spawn point)
├── Timer (fire rate cooldown)
└── HealthComponent (health_component.gd - optional)
```

**Base Script Responsibilities:**
- Detect enemies in range via Area2D signals
- Calculate target priority (closest/first-in-path)
- Handle firing logic (emit projectiles or apply damage)
- Emit signals on targeting/firing
- Handle animation/visual state

### NetworkNode Prefab Structure
```
Area2D (network_node.gd)
├── Sprite2D (visual - changes color based on state)
├── CollisionShape2D
├── Label (node ID/name)
├── AnimationPlayer (capture animation)
└── Timer (resource generation tick)
```

**Script Responsibilities:**
- Detect enemy contact (damage taken)
- Track capture progress
- Generate passive resources when owned
- Change visual state based on ownership

---

## 🔄 Key Systems Architecture

### 1. Pathfinding System
**Setup (done once at game start):**
1. NetworkMap (TileMapLayer) has physics layer for collision
2. Create NavigationRegion2D as child of NetworkMap
3. Assign NavigationPolygon with walkable areas defined
4. Bake navigation mesh

**Runtime (per enemy):**
1. Each enemy has NavigationAgent2D
2. Set target position: `agent.target_position = goal`
3. Each physics frame: `velocity = agent.get_next_path_position() - position`
4. Call: `move_and_slide()` to apply velocity

### 2. Tower Placement System
**Player Action:**
1. Click on owned/adjacent NetworkNode
2. Show tower selection UI (Firewall/Antivirus/PacketBomb)
3. Verify resources available
4. Instance tower scene at node position
5. Connect tower's Area2D signals to track enemies

**Tower Targeting:**
1. Area2D detects enemy entry → add to targets list
2. Area2D detects enemy exit → remove from targets list
3. Fire rate timer ticks → select best target → fire
4. Projectile/effect instantiated or damage applied directly

### 3. Wave Spawning System
**WaveManager Script:**
1. Waits for previous wave to complete
2. Calculates wave composition (how many Crawlers, Injectors, Overseers)
3. Spawns enemies at spawn point(s) with staggered timing
4. Tracks alive enemy count
5. When count reaches 0, completes wave
6. Triggers upgrade selection UI with timer for next wave
7. Repeats until all nodes are captured, then triggers final wave

### 4. Upgrade System
**Between Waves:**
1. When wave completes, GameStateManager emits `wave_completed()` starts timer for next wave
2. UpgradeSystem listens for signal, generates 3 random upgrade options
3. UpgradePanel shows 3 random upgrade options
4. Player clicks one
5. Applied to GameStateManager.upgrades_applied
6. Modifiers propagate to towers/enemies/resources via EventBus signal
7. Resume game

**Upgrade Data Format:**
```gdscript
class Upgrade:
    var name: String
    var description: String
    var effect_type: String  # "tower_damage", "enemy_health", etc.
    var modifier: float       # +0.2 = 20% increase
    var is_detrimental: bool
```

### 5. Resource Economy
**Generation:**
- Passive: Each owned node generates CPU/Bandwidth/Data per tick
- Active: Killing enemies grants resources
- Catching/capturing nodes grants resource burst

**Consumption:**
- Tower placement costs Data + Bandwidth
- Upgrades may require resource expenditure
- Resource shortage prevents certain actions

---

## 🎮 Input Handling

### Player Input (input_system.gd)
**Inputs to capture:**
- Left-click on NetworkNode → attempt tower placement
- Right-click on Tower → show options/destroy
- Spacebar → pause/resume
- ESC → pause menu

**Flow:**
1. Input detected in `_input()` handler
2. Raycast to find clicked Node
3. Emit appropriate EventBus signal
4. System responds to signal (place tower, etc.)

---

## 📊 Data Flow Example (Tower Fire)

```
1. WaveManager spawns enemy
2. Enemy appears in EnemyContainer
3. Tower's Area2D detects enemy entering range
4. Tower adds enemy to target list
5. Fire rate timer ticks
6. Tower selects closest enemy
7. Tower fires: emit EventBus.enemy_targeted(tower, enemy)
8. Projectile/effect instantiated
9. Collision detected → EventBus.enemy_damaged(enemy, damage)
10. Enemy health decreases
11. If health <= 0 → EventBus.enemy_died(enemy, tower)
12. Enemy scene removed from tree
13. WaveManager checks alive count
14. If count == 0 → EventBus.wave_completed()
15. Trigger upgrade panel and next wave timer
```

---

## 🔐 Save Data Structure (Minimal for MVP)

```gdscript
class SaveData:
    var run_uuid: String              # Unique run ID for leaderboard
    var final_score: int
    var waves_survived: int
    var towers_placed: int
    var enemies_killed: int
    var upgrades_used: Array[String]
    var final_health: int
    var timestamp: int
```

Stored locally in user:// directory, synced to Steam leaderboard in Week 3.

---

## 🎓 Design Patterns Used

| Pattern | Usage | Example |
|---------|-------|---------|
| **MVC** | Managers separate state/logic | GameStateManager = model |
| **Component** | Reusable behavior | HealthComponent attached to enemies/towers |
| **Singleton** | Global access | EventBus, AudioManager |
| **Object Pool** | Reuse instances | Projectiles spawned/despawned from pool |
| **Signal/Slot** | Loose coupling | EventBus signals between systems |
| **Factory** | Instance creation | Upgrade randomizer creates random upgrades |

---

## ⚙️ Physics & Collision Configuration

### Collision Layers
1. **Layer 1 (Towers):** Towers (static, block pathfinding)
2. **Layer 2 (Enemies):** Moving enemies (dynamic)
3. **Layer 3 (Environment):** Map obstacles
4. **Layer 4 (Nodes):** Capturable network nodes
5. **Layer 5 (Projectiles):** Towers' attacks (optional)

### Collision Masks
- **Enemies:** Detect layers 1, 3, 4 (avoid towers, obstacles, nodes)
- **Towers:** Detect layer 2 (target enemies)
- **Projectiles:** Detect layer 2 (hit enemies)

---

## 🧪 Testing Strategy

### Unit Tests (scripts/tests/)
- Tower damage calculation
- Resource economy balancing
- Upgrade modifier application
- Pathfinding validity

### Integration Tests
- Wave spawning sequence
- Tower placement validation
- Enemy death cascade

### Manual Testing (during dev)
- Play full run from start to finish
- Test pause/resume
- Verify no softlocks
- Check memory leaks during long play

---

## 🚀 Week 1–4 Architecture Milestones

| Week | Architecture Focus |
|------|-------------------|
| **Week 1** | Core scenes (Map, Enemy, Tower, Node), Basic systems (Pathfinding, Input, WaveManager) |
| **Week 2** | Resource economy, Upgrade system, UI integration |
| **Week 3** | Leaderboards (Steam), Menu scenes, Polish |
| **Week 4** | Final integration, build packaging, QA |

---

## 📋 Dependencies & Plugins

### Required
- **Godot 4.5.1** (free, open-source)

### Optional (Week 3+)
- **GodotSteam** (Steam integration)
- **Godot-Env** (for CI/CD)

### Asset Libraries
- **Kenney.nl** (free art)
- **Freesound** (free audio)

---

**Next Steps:** See `WEEK_1_TASK_BREAKDOWN.md` for detailed task assignments.
