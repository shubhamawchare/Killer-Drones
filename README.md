# 🎮 Killer Drones

> A single-player First Person Shooter built in **Unreal Engine 5** using the Blueprint visual scripting system.

![Unreal Engine](https://img.shields.io/badge/Unreal%20Engine-5.0-black?style=for-the-badge&logo=unrealengine&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![Genre](https://img.shields.io/badge/Genre-First%20Person%20Shooter-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📸 Screenshots

| Gameplay | Aggro Mode |
|----------|------------|
| ![Screenshot](Screenshot%202022-06-19%20121504.png) | Drone lights turn red when hit |

🎬 **[Watch Gameplay Video](Gameplay.mkv)**  
📄 **[Read Full Blackbook (PDF)](Killer%20Drones%20Blackbook.pdf)**

---

## 📖 About

**Killer Drones** is a BCA Final Year Project.

The player takes the role of **Leon**, an elite operative sent to North Korea to stop the villainous Diamond Co-Op from weaponising a newly discovered element capable of creating a supermassive black hole. Armed with the best gear on the planet, the player must survive waves of increasingly aggressive killer drones to save humanity.

Inspired by games like **Call of Duty: Warzone**, **Drone the Game**, **Assassin's Creed**, and **Thief** — with environmental art direction drawn from **Spider-Man PS4** and **Thief's** dark urban aesthetic.

---

## ✨ Features

- **Aggro System** — Drones switch to aggressive mode (lights turn red) when hit by bullets, directly chasing the player
- **Patrol AI** — Drones continuously patrol between waypoints using UE5's AI navigation system, maintaining constant pressure
- **Wave Difficulty** — Each wave spawns stronger drones with higher health and damage values
- **Consumable Pickups** — Health and ammo pickups scattered across the map for tactical resource management
- **HUD** — Live crosshair, health bar, ammo count, drone kill counter, and countdown timer
- **Timed Level** — Timer turns red below 10 seconds; failure state triggers if time runs out before all drones are eliminated
- **Win / Lose States** — "You Win!" and "You Died" screens with full input locking

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Unreal Engine 5.0 | Game engine & rendering |
| Blueprint Visual Scripting | All gameplay logic — zero C++ |
| UE5 AI / NavMesh | Drone patrol & aggro pathfinding |
| UMG (Widget Blueprints) | HUD — health bar, timer, ammo, crosshair |
| UE5 Marketplace Assets | Environment, weapon, and drone meshes |

---

## 🎮 Controls

| Key | Action |
|-----|--------|
| `W A S D` | Move |
| `Mouse` | Look / Aim |
| `Left Click` | Shoot |
| `Right Click` | Aim Down Sights |
| `Space` | Jump |

---

## 🧩 Blueprint Architecture

The game logic is entirely Blueprint-driven, structured across three main Blueprint classes:

### `FPS_Character` (Player)
The core player Blueprint handling all character behaviour:

| Function | Description |
|----------|-------------|
| `SpawnMuzzleFlash` | Spawns muzzle flash particle at burst point on fire |
| `SetAnimationBlueprint` | Casts and links the animation Blueprint to the character |
| `PlayFireMontage` | Plays the weapon firing animation montage |
| `FireWeapon` | Master fire function — muzzle flash, sound, line trace, damage, ammo decrement |
| `PerformLineTrace` | Raycast from camera; returns impact point and hit actor |
| `SetHUD` | Initialises the Character HUD widget — crosshair, timer, drone count |
| `SetHealth` | Updates the health progress bar (Health / MaxHealth) |
| `AddAmmo` | Increments ammo count when player overlaps an ammo pickup |
| `Heal` | Clamps and increases health when player overlaps a health pickup |

### `DronePawn` (Enemy AI)
| Function / Macro | Description |
|----------|-------------|
| `Construction Script` | Creates dynamic material instance for runtime colour changes |
| `Patrol` (Macro) | Moves drone between patrol points using `MoveToLocationOrActor` + `GetAIController` |
| `Explode` | Plays explosion sound & particle, then destroys the actor |
| `Event Graph` | Binds `OnTakeAnyDamage` — reduces health, triggers `Explode` at zero |
| Color Change | On bullet hit: `SetVectorParameterValue` turns drone lights red, drone pursues player via `MoveToGoalTarget` |

### `FPSGameMode` (Game Manager)
| Function | Description |
|----------|-------------|
| `StartGame` | Sets session state, enables input, clears warm-up UI |
| `UpdateWarmUpTimer` | 3-second "Clear Zone" countdown before game begins |
| `UpdateGameTimer` | Ticks countdown; turns timer text red below 10 seconds |
| `DroneDied` | Decrements drone count; calls `PlayerWon` when count reaches zero |
| `PlayerWon` | Displays "You Win!", locks input, sets session state |
| `PlayerDied` | Displays "You Died", locks input |
| `OutOfTime` | Triggers on timer expiry; displays time-out message |
| `TimeRemainingFormat` | Formats remaining time as MM:SS |

---

## ⚙️ Minimum System Requirements (Play)

| Component | Requirement |
|-----------|-------------|
| OS | Windows 7 / 8 / 8.1 / 10 |
| RAM | 4 GB |
| GPU | DirectX 9 compatible |

## ⚙️ Development Machine

| Component | Spec |
|-----------|------|
| CPU | AMD Ryzen 9 5900X |
| RAM | 16 GB |
| GPU | NVIDIA RTX 3080 |
| OS | Windows 10 |

---

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/shubhamawchare/Killer-Drones.git
   ```
2. Install **Unreal Engine 5.0** via the [Epic Games Launcher](https://www.unrealengine.com)
3. Open `FirstPersonShooter.uproject` with UE5
4. Click **Play** in the editor, or package for Windows via `File → Package Project → Windows`

> **Note:** Git LFS is required to clone the full project with assets. Run `git lfs install` before cloning.

---

## 📁 Project Structure

```
Killer-Drones/
├── Config/              # Engine and game configuration files
├── Content/             # All game assets (tracked via Git LFS)
│   ├── Blueprints/      # FPS_Character, DronePawn, FPSGameMode
│   ├── Maps/            # FPSLevel
│   ├── Animations/      # Weapon fire montage, character anims
│   └── ...
├── FirstPersonShooter.uproject
├── Gameplay.mp4         # Gameplay recording
└── Killer Drones Blackbook.pdf   # Full project report
```

---

## 👤 Developer

**Shubham Awchare**  
BCA — Game & Mobile Software Development  
Tilak Maharashtra Vidyapeeth, Pune | 2019–2022  

[![GitHub](https://img.shields.io/badge/GitHub-shubhamawchare-181717?style=flat-square&logo=github)](https://github.com/shubhamawchare)

---

## 📚 References

- Unreal Engine 5 Documentation — [docs.unrealengine.com](https://docs.unrealengine.com/5.0/en-US/)
- Reference games: Drone the Game, Call of Duty: Warzone, Assassin's Creed, Thief, Spider-Man PS4
- Concept inspiration: Spider-Man: Far From Home, The Bourne Legacy
- Learning resources: YouTube, Udemy, Unreal Engine Forums
