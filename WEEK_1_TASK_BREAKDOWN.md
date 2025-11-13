# 📅 Week 1 Task Breakdown: Network Breach Core Prototype

## Week 1 Goal
**Build a working core loop prototype where enemies spawn, pathfind through a map, towers shoot them, and you survive waves.**

**Deliverable:** Playable single-wave demo with 1 tower type, 1 enemy type, basic UI.

---

## Daily Schedule Overview

| Day | Focus | Tasks | Estimate |
|-----|-------|-------|----------|
| **Mon-Tue** | **Project Setup & Map** | Folder structure, Godot config, create base map, test tilemap | 16 hrs |
| **Wed** | **Pathfinding & Navigation** | Set up NavigationRegion2D, create enemy base scene, test pathfinding | 8 hrs |
| **Thu** | **Enemy Movement** | Script NavigationAgent2D movement, test walking | 6 hrs |
| **Fri** | **Tower Basics** | Create tower scene, implement targeting, basic firing | 8 hrs |
| **Sat-Sun** | **Wave System & Polish** | Implement WaveManager, basic UI, first playable build, bug fixes | 12 hrs |

**Total: ~50 hours (doable 1 full work week)**

---

## 🔴 Day 1–2: Project Setup & Map Foundation

### Objectives
- ✅ Set up Godot project folder structure
- ✅ Configure Godot project settings (resolution, physics, input)
- ✅ Create NetworkMap TileMapLayer with test tiles
- ✅ Set up sprite assets (placeholder geometry)
- ✅ Commit to git

### Tasks

#### 2.1 Create Folder Structure
**Task:** Set up `/assets`, `/scenes`, `/scripts`, `/addons` directories  
**Subtasks:**
- [x] Create `assets/sprites/towers/`, `assets/sprites/enemies/`, `assets/sprites/nodes/`, `assets/sprites/fx/`
- [x] Create `assets/sounds/sfx/`, `assets/sounds/music/`
- [x] Create `assets/fonts/`, `assets/data/`
- [x] Create `scenes/game/`, `scenes/ui/`, `scenes/menus/`
- [x] Create `scripts/managers/`, `scripts/systems/`, `scripts/components/`, `scripts/data/`, `scripts/events/`

**Godot Tools:** File system explorer, use Godot's file browser  
**Time:** 30 min ✅ COMPLETE

---

#### 2.2 Configure Project Settings
**Task:** Set Godot physics, rendering, input, and display settings  
**Subtasks:**
- [x] Set resolution to 1920x1080
- [x] Enable physics 2D
- [x] Create input map entries:
  - [x] `ui_click_left` → Mouse Button Left
  - [x] `ui_click_right` → Mouse Button Right
  - [x] `ui_pause` → Spacebar
- [x] Set default physics gravity to (0, 0) — tower defense, not platformer
- [x] Disable V-Sync (for faster iteration)

**Godot Path:** Project → Project Settings → General/Input Map/Physics  
**Time:** 30 min ✅ COMPLETE

---

#### 2.3 Create Map TileSet & TileMapLayer
**Task:** Create a simple TileSet with placeholder tiles, then create NetworkMap TileMapLayer  
**Subtasks:**

**Step A: Create TileSet Resource**
- [ ] Create new TileSet resource: `assets/tilesets/network_map_tileset.tres`
- [ ] Open TileSet editor
- [ ] Create a single "Ground" tile (32x32 or 64x64 pixels)
  - Use simple green rectangle for now (placeholder)
  - Export/import as PNG to `assets/sprites/`
- [ ] Set up texture in TileSet
- [ ] Define physics layer (no collision needed for ground)
- [ ] Define custom data layer for "tower_placement_allowed" (bool)

**Step B: Create NetworkMap Scene**
- [ ] Create new scene: `scenes/game/map/network_map.tscn`
- [ ] Add TileMapLayer node as root
- [ ] Assign tileset
- [ ] Draw a 10x10 test map in the TileMapLayer editor
- [ ] Save scene

**Godot Docs:** [TileSet tutorial](https://docs.godotengine.org/en/stable/tutorials/2d/using_tilesets.html), [TileMapLayer](https://docs.godotengine.org/en/stable/tutorials/2d/using_tilemaps.html)  
**Time:** 2 hrs

---

#### 2.4 Create Placeholder Sprites (Geometric Shapes)
**Task:** Create simple PNG files for towers, enemies, nodes using Godot's built-in drawing or external tool  
**Subtasks:**
- [ ] Tower sprite: Blue circle (64x64 px)
- [ ] Enemy sprite: Red circle (32x32 px)
- [ ] Captured node sprite: Cyan circle (48x48 px)
- [ ] Locked node sprite: Gray circle (48x48 px)

**Tools:** Use Aseprite, GIMP, or Pixel Lab AI; save as PNG to `assets/sprites/`  
**Tip:** For now, just use colored circles—no fancy art  
**Time:** 1 hr

---

#### 2.5 Create Main Game Scene Structure
**Task:** Create base scene hierarchy: Main → World + GUI  
**Subtasks:**
- [ ] Create `scenes/game/main.tscn`
  - Root: Node (name: "Main")
  - Child: Node2D (name: "World")
  - Child: Control (name: "GUI")
- [ ] Save scene
- [ ] Instance NetworkMap into World as child
- [ ] Create empty `scripts/main.gd` (attach to Main node)
- [ ] Create empty `scenes/game/world.gd` (attach to World node)

**File Structure:**
```
scenes/game/
├── main.tscn
├── main.gd
├── world.tscn
├── world.gd
└── map/
    ├── network_map.tscn
```

**Time:** 1 hr

---

#### 2.6 Commit & Checkpoint
**Task:** Save all work to git with clear commit message  
**Command:**
```bash
cd C:\Users\rivie\GoDotProjects\network-breach
git add -A
git commit -m "Day 1-2: Project setup, folder structure, base map scene"
```

**Time:** 15 min

---

## 🟡 Day 3: Pathfinding & Enemy Setup

### Objectives
- ✅ Create NavigationRegion2D with navigation mesh
- ✅ Create Enemy base scene with CharacterBody2D + NavigationAgent2D
- ✅ Test enemy navigation (no movement yet, just structure)

### Tasks

#### 3.1 Set Up Navigation Mesh
**Task:** Add NavigationRegion2D to NetworkMap, define walkable areas  
**Subtasks:**
- [ ] Add NavigationRegion2D as child of NetworkMap TileMapLayer
- [ ] Create new NavigationPolygon resource: `scenes/game/map/network_paths.tres`
- [ ] Assign NavigationPolygon to NavigationRegion2D
- [ ] In NavigationPolygon editor:
  - [ ] Draw polygon around entire map (define walkable area)
  - [ ] Ensure polygon doesn't overlap obstacles
- [ ] Test: Bake navigation mesh (should show in editor)
- [ ] Verify navigation mesh renders correctly

**Godot Docs:** [NavigationAgent2D](https://docs.godotengine.org/en/stable/classes/class_navigationagent2d.html), [Navigation 2D](https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_introduction_2d.html)  
**Time:** 1.5 hrs

---

#### 3.2 Create Enemy Base Scene
**Task:** Build reusable enemy prefab structure  
**Subtasks:**
- [ ] Create `scenes/game/enemies/enemy_base.tscn`
- [ ] Scene structure:
  ```
  CharacterBody2D (enemy_base.gd)
  ├── Sprite2D
  ├── CollisionShape2D (CircleShape2D, radius 16px)
  └── NavigationAgent2D
  ```
- [ ] Attach Sprite2D to placeholder enemy PNG
- [ ] Set collision shape to circular (radius appropriate for sprite)
- [ ] Configure NavigationAgent2D:
  - [ ] Set `navigation_layers` to match NavigationRegion2D layer
  - [ ] Set `target_desired_distance` to 10.0
  - [ ] Set `path_desired_distance` to 20.0
  - [ ] Enable `avoidance_enabled` (optional, for multi-enemy cases)
- [ ] Save scene

**File:** `scenes/game/enemies/enemy_base.tscn`  
**Time:** 1.5 hrs

---

#### 3.3 Create Enemy Movement Script Skeleton
**Task:** Create GDScript for enemy movement (no movement yet, just structure)  
**Subtasks:**
- [ ] Create `scripts/enemy_base.gd`
- [ ] Attach to CharacterBody2D in enemy_base.tscn
- [ ] Write skeleton code:
  ```gdscript
  extends CharacterBody2D

  @export var speed: float = 100.0
  @onready var nav_agent = $NavigationAgent2D
  @onready var sprite = $Sprite2D

  var target_position: Vector2 = Vector2.ZERO

  func _ready():
      print("Enemy spawned at ", global_position)

  func _physics_process(delta):
      # Will implement movement next day
      pass

  func set_target(pos: Vector2):
      target_position = pos
      nav_agent.target_position = target_position

  func _on_navigation_finished():
      print("Enemy reached target")
  ```
- [ ] Save script

**Time:** 30 min

---

#### 3.4 Test Navigation Setup
**Task:** Instance test enemy in map, verify no errors  
**Subtasks:**
- [ ] Open main.tscn
- [ ] Manually add enemy_base.tscn instance to World/NetworkMap
- [ ] Play scene (F5)
- [ ] Verify:
  - [ ] Enemy appears on screen
  - [ ] No errors in console
  - [ ] NavigationAgent2D path visible (debug draw if available)
- [ ] Stop play

**Time:** 30 min

---

#### 3.5 Commit
**Task:** Commit pathfinding setup  
**Command:**
```bash
git add -A
git commit -m "Day 3: Navigation setup, enemy base scene, pathfinding skeleton"
```

**Time:** 15 min

---

## 🟡 Day 4: Enemy Movement Implementation

### Objectives
- ✅ Implement enemy movement along navigation path
- ✅ Test enemy walking across map
- ✅ Verify pathfinding works correctly

### Tasks

#### 4.1 Implement Enemy Movement Loop
**Task:** Complete enemy_base.gd to move along navigation path  
**Subtasks:**
- [ ] Update `_physics_process(delta)` to:
  ```gdscript
  func _physics_process(delta):
      if not nav_agent.is_navigation_finished():
          var next_path_pos = nav_agent.get_next_path_position()
          var direction = (next_path_pos - global_position).normalized()
          velocity = direction * speed
          move_and_slide()
      else:
          velocity = Vector2.ZERO
  ```
- [ ] Add signal for reaching destination:
  ```gdscript
  signal reached_destination

  func _physics_process(delta):
      # ... existing code ...
      if nav_agent.is_navigation_finished() and velocity == Vector2.ZERO:
          reached_destination.emit()
  ```
- [ ] Test by calling `enemy.set_target(Vector2(500, 500))`

**Godot Docs:** [CharacterBody2D](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html#class-characterbody2d-method-move-and-slide)  
**Time:** 1 hr

---

#### 4.2 Create Enemy Spawner Script (Simplified)
**Task:** Create temporary spawner to test enemies walking  
**Subtasks:**
- [ ] Create `scripts/systems/temp_enemy_spawner.gd`
- [ ] Attach to World node
- [ ] Write code to spawn enemy at point A, target point B:
  ```gdscript
  extends Node2D

  @export var enemy_scene: PackedScene
  @export var spawn_point: Vector2 = Vector2(100, 100)
  @export var target_point: Vector2 = Vector2(400, 400)

  func _ready():
      var enemy = enemy_scene.instantiate()
      add_child(enemy)
      enemy.global_position = spawn_point
      enemy.set_target(target_point)
  ```
- [ ] Assign enemy_base.tscn to `enemy_scene` export variable in inspector
- [ ] Save script

**Time:** 30 min

---

#### 4.3 Test Enemy Movement
**Task:** Verify enemy walks from A to B  
**Subtasks:**
- [ ] Delete manual enemy instance from main.tscn
- [ ] Add Node2D child to World
- [ ] Attach temp_enemy_spawner.gd to it
- [ ] Set spawn_point and target_point in inspector
- [ ] Play scene
- [ ] Verify:
  - [ ] Enemy spawns at spawn_point
  - [ ] Enemy moves toward target_point
  - [ ] Enemy follows navigation path (not straight line)
  - [ ] Enemy stops at target_point
- [ ] Stop play

**Time:** 1 hr

---

#### 4.4 Polish & Debug
**Task:** Fix any movement issues, smooth out visuals  
**Subtasks:**
- [ ] If enemy overshoots target, increase `path_desired_distance`
- [ ] If enemy moves too fast/slow, adjust `speed` export variable
- [ ] Add sprite rotation to face movement direction (optional):
  ```gdscript
  if velocity != Vector2.ZERO:
      sprite.rotation = velocity.angle()
  ```
- [ ] Test with multiple enemies (spawn 3, verify no collision issues)

**Time:** 1 hr

---

#### 4.5 Commit
**Task:** Commit enemy movement  
**Command:**
```bash
git add -A
git commit -m "Day 4: Enemy movement implementation, pathfinding working"
```

**Time:** 15 min

---

## 🔵 Day 5: Tower Basics & Targeting

### Objectives
- ✅ Create Tower base scene with Area2D for targeting
- ✅ Implement tower targeting logic (find closest enemy)
- ✅ Implement basic firing (visual effect for now)

### Tasks

#### 5.1 Create Tower Base Scene
**Task:** Build reusable tower prefab  
**Subtasks:**
- [ ] Create `scenes/game/towers/tower_base.tscn`
- [ ] Scene structure:
  ```
  Node2D (tower_base.gd)
  ├── Sprite2D (tower visual)
  ├── Area2D (attack range detector)
  │   └── CollisionShape2D (CircleShape2D for range)
  ├── Marker2D (projectile spawn point)
  └── Timer (fire rate)
  ```
- [ ] Attach tower sprite (blue circle)
- [ ] Set Area2D collision shape to large circle (attack range = 200px)
- [ ] Position Marker2D at center of tower
- [ ] Configure Timer:
  - [ ] Set wait_time to 1.0 seconds (fire rate)
  - [ ] Set one_shot to false
  - [ ] Connect timeout() signal to tower firing logic
- [ ] Save scene

**File:** `scenes/game/towers/tower_base.tscn`  
**Time:** 1 hr

---

#### 5.2 Create Tower Script with Targeting
**Task:** Implement targeting logic  
**Subtasks:**
- [ ] Create `scripts/tower_base.gd`:
  ```gdscript
  extends Node2D

  @export var damage: float = 10.0
  @export var fire_rate: float = 1.0
  @onready var range_detector: Area2D = $Area2D
  @onready var fire_timer: Timer = $Timer
  @onready var sprite = $Sprite2D

  var targets_in_range: Array = []
  var current_target = null

  func _ready():
      # Connect Area2D signals
      range_detector.body_entered.connect(_on_target_entered)
      range_detector.body_exited.connect(_on_target_exited)
      
      # Connect fire timer
      fire_timer.wait_time = fire_rate
      fire_timer.timeout.connect(_on_fire_timer_timeout)
      fire_timer.start()

  func _on_target_entered(body):
      if body.is_in_group("enemies"):
          targets_in_range.append(body)
          print("Enemy in range: ", body)

  func _on_target_exited(body):
      if body.is_in_group("enemies"):
          targets_in_range.erase(body)
          if current_target == body:
              current_target = null

  func _on_fire_timer_timeout():
      # Select closest target
      if not targets_in_range.is_empty():
          current_target = targets_in_range[0]
          for target in targets_in_range:
              if target.global_position.distance_to(global_position) < \
                 current_target.global_position.distance_to(global_position):
                  current_target = target
          
          if current_target:
              _fire_at_target(current_target)

  func _fire_at_target(target):
      print("Tower firing at ", target)
      # TODO: Create projectile/visual effect
      # For now, just reduce enemy health directly
      if target.has_method("take_damage"):
          target.take_damage(damage)
  ```
- [ ] Attach to Node2D in tower_base.tscn
- [ ] Save

**Time:** 1.5 hrs

---

#### 5.3 Add Health Component to Enemy
**Task:** Implement take_damage() method on enemies  
**Subtasks:**
- [ ] Update enemy_base.gd:
  ```gdscript
  var health: float = 50.0
  var max_health: float = 50.0

  func take_damage(damage: float):
      health -= damage
      print("Enemy damaged. Health: ", health)
      if health <= 0:
          die()

  func die():
      print("Enemy died")
      queue_free()  # Remove from scene
  ```
- [ ] Test: Enemy should disappear when damaged enough

**Time:** 30 min

---

#### 5.4 Set Up Enemy Group
**Task:** Ensure enemies are tagged so towers can detect them  
**Subtasks:**
- [ ] In enemy_base.gd `_ready()`, add:
  ```gdscript
  add_to_group("enemies")
  ```
- [ ] Verify tower can now detect enemies

**Time:** 15 min

---

#### 5.5 Test Tower Targeting
**Task:** Verify tower fires at enemy  
**Subtasks:**
- [ ] Update main.tscn:
  - [ ] Add tower_base.tscn instance to World
  - [ ] Position at center of map
- [ ] Play scene
- [ ] Verify:
  - [ ] Enemy walks into tower range
  - [ ] Tower starts firing (console shows "Tower firing at...")
  - [ ] Enemy takes damage and dies
  - [ ] Enemy disappears when health reaches 0
- [ ] Stop play

**Time:** 1 hr

---

#### 5.6 Commit
**Task:** Commit tower system  
**Command:**
```bash
git add -A
git commit -m "Day 5: Tower scene, targeting logic, enemy health"
```

**Time:** 15 min

---

## 🟢 Day 6–7: Wave System & Playable Build

### Objectives
- ✅ Create WaveManager to spawn enemy waves
- ✅ Implement basic HUD (health, resources, wave timer)
- ✅ Create playable end-to-end experience
- ✅ Polish and bug fixes

### Tasks

#### 6.1 Create Wave Manager Script
**Task:** Implement spawning system  
**Subtasks:**
- [ ] Create `scripts/systems/wave_manager.gd`:
  ```gdscript
  extends Node

  @export var enemy_scene: PackedScene
  @export var spawn_point: Vector2 = Vector2(100, 100)
  @export var target_point: Vector2 = Vector2(400, 400)
  @export var spawn_interval: float = 1.5  # seconds between spawns

  var current_wave: int = 1
  var enemies_spawned_this_wave: int = 0
  var max_enemies_per_wave: int = 3
  var enemies_alive: int = 0
  var is_wave_active: bool = false

  signal wave_started(wave_number)
  signal wave_completed()
  signal enemy_spawned(enemy)
  signal enemy_died(enemy)

  func _ready():
      # Start first wave after delay
      await get_tree().create_timer(1.0).timeout
      start_wave()

  func start_wave():
      current_wave += 1
      enemies_spawned_this_wave = 0
      max_enemies_per_wave = 2 + current_wave  # Difficulty scales
      is_wave_active = true
      wave_started.emit(current_wave)
      print("Wave %d started" % current_wave)
      _spawn_next_enemy()

  func _spawn_next_enemy():
      if enemies_spawned_this_wave < max_enemies_per_wave and is_wave_active:
          var enemy = enemy_scene.instantiate()
          add_child(enemy)
          enemy.global_position = spawn_point
          enemy.set_target(target_point)
          enemy.died.connect(_on_enemy_died)  # Connect to enemy death signal
          enemies_alive += 1
          enemies_spawned_this_wave += 1
          enemy_spawned.emit(enemy)
          print("Enemy spawned: %d/%d" % [enemies_spawned_this_wave, max_enemies_per_wave])
          
          # Schedule next spawn
          await get_tree().create_timer(spawn_interval).timeout
          _spawn_next_enemy()

  func _on_enemy_died(enemy):
      enemies_alive -= 1
      enemy_died.emit(enemy)
      print("Enemy died. Alive: %d" % enemies_alive)
      
      if enemies_alive == 0 and enemies_spawned_this_wave >= max_enemies_per_wave:
          wave_completed.emit()
          print("Wave %d completed!" % current_wave)
          await get_tree().create_timer(2.0).timeout
          start_wave()
  ```
- [ ] Save script
- [ ] Attach to World node in main.tscn

**Time:** 1.5 hrs

---

#### 6.2 Add `died` Signal to Enemy
**Task:** Make enemy emit signal when dead  
**Subtasks:**
- [ ] Update enemy_base.gd:
  ```gdscript
  signal died

  func die():
      print("Enemy died")
      died.emit()  # Emit signal
      queue_free()
  ```

**Time:** 15 min

---

#### 6.3 Create Basic HUD UI Scene
**Task:** Build in-game UI (health, wave counter)  
**Subtasks:**
- [ ] Create `scenes/ui/hud.tscn`
- [ ] Scene structure:
  ```
  Control (hud.gd)
  ├── HBoxContainer
  │   ├── Label (health_display) - "Health: 100"
  │   ├── Label (wave_display) - "Wave: 1"
  │   └── Label (resources_display) - "Data: 100"
  ```
- [ ] Create `scripts/hud.gd`:
  ```gdscript
  extends Control

  @onready var health_label = $HBoxContainer/HealthLabel
  @onready var wave_label = $HBoxContainer/WaveLabel
  @onready var resources_label = $HBoxContainer/ResourcesLabel

  func _ready():
      update_health(100)
      update_wave(1)
      update_resources(100)

  func update_health(amount):
      health_label.text = "Health: %d" % amount

  func update_wave(wave):
      wave_label.text = "Wave: %d" % wave

  func update_resources(amount):
      resources_label.text = "Data: %d" % amount
  ```
- [ ] Save scene and script

**Time:** 1 hr

---

#### 6.4 Create Game State Manager (Simplified)
**Task:** Track game state (health, wave, resources)  
**Subtasks:**
- [ ] Create `scripts/managers/game_state_manager.gd`:
  ```gdscript
  extends Node

  var health: int = 100
  var current_wave: int = 1
  var resources: int = 100

  signal health_changed(new_health)
  signal wave_changed(new_wave)
  signal resources_changed(new_resources)

  func take_damage(amount: int):
      health -= amount
      health_changed.emit(health)
      if health <= 0:
          game_over(false)

  func set_wave(wave: int):
      current_wave = wave
      wave_changed.emit(wave)

  func add_resources(amount: int):
      resources += amount
      resources_changed.emit(resources)

  func game_over(victory: bool):
      print("Game Over - Victory: ", victory)
      get_tree().paused = true
  ```
- [ ] Register as Autoload: Project Settings → Autoload → Add script as "GameState"

**Time:** 1 hr

---

#### 6.5 Connect Signals Between Systems
**Task:** Wire up game state updates  
**Subtasks:**
- [ ] In world.gd, connect wave_manager signals:
  ```gdscript
  extends Node2D

  @onready var wave_manager = $WaveManager
  @onready var hud = $HUD
  @onready var game_state = GameState  # Autoload

  func _ready():
      wave_manager.wave_started.connect(_on_wave_started)

  func _on_wave_started(wave_number):
      game_state.set_wave(wave_number)
      hud.update_wave(wave_number)
  ```
- [ ] Test: HUD should update when wave starts

**Time:** 30 min

---

#### 6.6 Add Simple Win/Loss Condition
**Task:** Implement end-game logic  
**Subtasks:**
- [ ] When all enemies die and waves complete → Victory
- [ ] When health reaches 0 → Defeat
- [ ] Create `scenes/ui/game_over_screen.tscn`:
  ```
  Control
  ├── ColorRect (semi-transparent overlay)
  ├── VBoxContainer
  │   ├── Label ("VICTORY" or "DEFEAT")
  │   ├── Label (stats)
  │   ├── Button (Restart)
  │   └── Button (Menu)
  ```
- [ ] Wire restart button to reload scene: `get_tree().reload_current_scene()`

**Time:** 1.5 hrs

---

#### 6.7 Test Full Playable Build
**Task:** Play full game loop end-to-end  
**Subtasks:**
- [ ] Open main.tscn
- [ ] Play (F5)
- [ ] Verify:
  - [ ] Enemy spawns at wave start
  - [ ] Enemy walks toward goal
  - [ ] Tower shoots enemy
  - [ ] Enemy dies and disappears
  - [ ] Wave completes after all enemies dead
  - [ ] Next wave spawns with more enemies
  - [ ] HUD updates correctly
  - [ ] Game feels playable (not boring, not impossible)
- [ ] Play for 10+ minutes, note any bugs
- [ ] Stop play

**Expected Duration:** 20–30 min play test + bug fixes

---

#### 6.8 Bug Fixes & Polish (Sunday)
**Task:** Fix crashes, improve feel  
**Subtasks:**
- [ ] Fix any softlocks (waves not progressing, etc.)
- [ ] Adjust enemy speed if too slow/fast
- [ ] Adjust tower fire rate if boring/overwhelming
- [ ] Tune enemy health vs tower damage (should be satisfying)
- [ ] Add minimal SFX if time permits (just placeholder)
- [ ] Test pause (Spacebar) — optional for MVP

**Time:** 2–3 hrs

---

#### 6.9 Final Commit & Build
**Task:** Commit final Week 1 build  
**Command:**
```bash
git add -A
git commit -m "Day 6-7: Wave system, HUD, game over screen, playable prototype"
```

**Time:** 15 min

---

## 📋 Week 1 Acceptance Criteria

### Functionality ✅
- [ ] Enemy spawns at wave start
- [ ] Enemy pathfinds across map correctly
- [ ] Tower detects enemy in range
- [ ] Tower fires and damages enemy
- [ ] Enemy dies when health reaches 0
- [ ] Multiple waves spawn with increasing difficulty
- [ ] Game ends in victory when waves complete
- [ ] HUD displays health, wave, resources

### Code Quality ✅
- [ ] No console errors during normal gameplay
- [ ] Scripts follow GDScript conventions
- [ ] Scenes are properly organized in folders
- [ ] Signals used for loose coupling (not direct references)

### Playability ✅
- [ ] Game is playable for 10+ minutes without crash
- [ ] Gameplay loop is clear (spawn → defend → advance)
- [ ] No obvious balance issues

---

## 🎯 Next Steps (Week 2 Preview)

Once Week 1 is complete:
- **Network expansion mechanic** (capturing nodes)
- **Resource economy** (Data, Bandwidth, CPU generation)
- **Multiple tower types** (Firewall, Antivirus, PacketBomb)
- **Upgrade system** (3 choices between waves)
- **Leaderboard hook** (save score)

---

## 🚨 Common Pitfalls to Avoid

| Pitfall | How to Avoid |
|---------|-------------|
| Scope creep | Stick to 1 tower, 1 enemy type. NO fancy art, NO extra features. |
| Over-engineering | Use simple solutions first. Refactor only if needed. |
| Not testing | Play the build frequently. Bugs compound. |
| Perfectionism | Placeholder art/sounds are OK. Iterate post-launch. |
| Losing motivation | Celebrate small wins. After Day 3 you have movement working—that's huge! |

---

**Good luck! You've got this. 🚀**
