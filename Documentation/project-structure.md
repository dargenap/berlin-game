# Berlin Game — Project Structure

This document defines the folder structure and organization rules for the project.

Goals:

- keep the project scalable
- keep gameplay systems separated
- keep assets easy to locate
- maintain consistent naming and organization


---

# Root Project Structure

The root directory contains everything related to the project, not only the Unreal project itself.

```bash
BerlinGame/
├── UnrealProject/        # Unreal Engine project (Content, Config, .uproject)
├── Assets_Source/        # source assets (Blender, Substance, etc.)
├── Assets_Export/        # exported FBX and textures ready for UE import
├── Audio_Source/         # raw audio recordings and editing sessions
├── Documentation/        # design docs, structure rules, naming conventions
├── References/           # concept art, visual references, inspiration
├── Marketing/            # screenshots, trailers, promotional material
└── Backup/               # manual project backups
```

---

# Unreal Engine Content Structure

All project assets must live inside the `Berlin` root folder.

```bash
Content/
├── Berlin/              # all assets belonging to the game
├── External/            # marketplace / third-party assets
├── __ExternalActors__/  # UE world partition system folder
├── __ExternalObjects__/ # UE world partition system folder
├── Collections/         # editor collections
└── Developers/          # personal dev folders
```

---

# Berlin Folder Structure

```bash
Berlin/
├── Core/             # shared systems used across the game
├── Characters/       # player and NPC characters
├── Weapons/          # firearms and melee weapons
├── Items/            # consumables and equipment
├── AI/               # AI systems
├── World/            # environment and world modules
├── Audio/            # sound effects and music
├── UI/               # user interface assets
├── VFX/              # particle and visual effects
├── Data/             # data assets and tables
├── Maps/             # playable levels
└── Dev/              # testing and prototypes
```

## Purpose

Top-level folders represent **gameplay systems** rather than asset types.

---

# Core Systems

Contains shared gameplay systems used across the entire game.

```bash
Core/
├── Blueprints/          # base gameplay systems
├── Interfaces/          # blueprint interfaces
├── Enums/               # shared enums
├── Structs/             # shared data structures
├── Materials/           # master materials
└── Functions/           # blueprint function libraries
```

## Example Assets

| Asset            | Purpose               |
| ---------------- | --------------------- |
| BP_GameMode      | main game mode        |
| BP_GameInstance  | global game state     |
| BPI_Interactable | interaction interface |
| E_WeaponType     | weapon type enum      |
| ST_WeaponStats   | weapon stat struct    |

---

# Characters

All character-related assets are stored here.

```bash
Characters/
├── Player/
├── Police/
├── Raiders/
├── Militia/
└── Common/
```

## Example Player Structure

```bash
Characters/Player/
├── BP/                  # player blueprints
├── Mesh/                # skeletal meshes
├── Animations/          # animation assets
├── Materials/           # character materials
└── Audio/               # voice and foley
```

---

# Weapons

Weapons are grouped by category.

```bash
Weapons/
├── Core/                # weapon base classes
├── Firearms/            # guns
├── Melee/               # melee weapons
└── Utility/             # grenades and gadgets
```

## Example Firearm Structure

```bash
Weapons/Firearms/Makarov/
├── BP/                  # weapon blueprint
├── Mesh/                # weapon mesh
├── Materials/           # weapon materials
├── Audio/               # firing and reload sounds
└── Data/                # weapon data assets
```

## Example Melee Weapon

```bash
Weapons/Melee/Crowbar/
├── BP/                  # weapon blueprint
├── Mesh/                # weapon mesh
├── Materials/           # weapon materials
├── Audio/               # impact sounds
└── Data/                # weapon stats
```

---

# AI

AI logic and behavior systems.

```bash
AI/
├── BehaviorTrees/       # behavior tree assets
├── Blackboards/         # AI data storage
├── Tasks/               # behavior tree tasks
├── Services/            # behavior tree services
├── Decorators/          # behavior conditions
└── Perception/          # AI perception configuration
```

---

# World / Environment

Environment assets and world modules.

```bash
World/
├── Environment/         # terrain and landscapes
├── Buildings/           # building modules
├── Props/               # environmental props
├── Foliage/             # vegetation
├── Weather/             # weather systems
├── Lighting/            # lighting setups
└── Landmarks/           # unique locations
```

## Example Building Structure

```bash
World/Buildings/Altbau/
├── Mesh/
├── Materials/
├── Textures/
└── Blueprints/
```

---

# Maps

Maps are separated by development stage.

```bash
Maps/
├── Prototype/           # early experiments
├── Test/                # testing maps
├── Main/                # playable levels
└── Sublevels/           # streamed level parts
```

---

# Data

Gameplay configuration assets.

```bash
Data/
├── Weapons/
├── Items/
├── Factions/
├── Loot/
└── World/
```

These assets control gameplay balance.

---

# Dev Folder

The Dev folder is used for temporary content and experiments.

```bash
Dev/
├── TestMaps/
├── DebugTools/
└── Experiments/
```

## Rule

Prototype assets must remain here until they are production-ready.

---

# External Assets

Marketplace and third-party assets remain outside the main game folder.

```bash
External/
├── Marketplace/
├── Quixel/
└── Placeholder/
```

Assets are only moved into `Berlin` once they are actively used.

---

# Folder Organization Principle

Top-level structure:

```
system / feature based
```

Inside those folders:

```
asset type based
```

Example:

```bash
Weapons/Firearms/Makarov/Mesh
Weapons/Firearms/Makarov/Audio
Weapons/Firearms/Makarov/BP
```

---

# Guiding Principle

When navigating the project, the main question should be:

> **Which gameplay system does this asset belong to?**

instead of

> **What asset type is this?**

This structure allows the project to scale to **hundreds or thousands of assets without chaos**.
