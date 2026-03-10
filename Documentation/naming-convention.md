# Berlin Game — Naming Conventions

This document defines the naming conventions used across the project.

Goals:

- maintain consistent naming across the project
- allow easy searching and filtering
- prevent naming conflicts
- support large scale project growth


---

# General Naming Rules

All assets must follow these rules:

| Rule | Description |
|-----|-----|
| lowercase for IDs | IDs always use lowercase |
| underscores | use `_` instead of spaces |
| no spaces | spaces break automation and tools |
| descriptive names | names should clearly describe the asset |
| consistent prefixes | UE assets always use prefixes |

Example:

```

f-p-pipe_shotgun

```

Incorrect:

```

f-p-PipeShotgun
Pipe Shotgun

```

---

# Unreal Engine Asset Naming

Unreal assets use **prefix-based naming**.

Format:

```

PREFIX_AssetName

```

Example:

```

BP_PlayerCharacter
SM_WPN_Crowbar
T_WPN_AKM_D

```

---

# Blueprint Naming

| Prefix | Asset Type |
|------|------|
| BP_ | Blueprint Actor |
| WBP_ | Widget Blueprint |
| ABP_ | Animation Blueprint |
| BPI_ | Blueprint Interface |
| BPFL_ | Blueprint Function Library |

Examples:

```

BP_PlayerCharacter
BP_WPN_AKM
WBP_Inventory
ABP_Player
BPI_Interactable

```

---

# Data Asset Naming

| Prefix | Type |
|------|------|
| DA_ | Data Asset |
| DT_ | Data Table |

Examples:

```

DA_WPN_AKM
DA_Item_Medkit
DT_LootTable
DT_FactionData

```

---

# Enum Naming

Enums use prefix:

```

E_

```

Examples:

```

E_WeaponType
E_EquipSlot
E_Faction
E_ItemType

```

---

# Struct Naming

Structs use prefix:

```

ST_

```

Examples:

```

ST_WeaponStats
ST_InventoryItem
ST_FactionRelation

```

---

# Static Mesh Naming

| Prefix | Description |
|------|------|
| SM_ | Static Mesh |

Examples:

```

SM_WPN_Crowbar
SM_PROP_Barrel
SM_BLD_WindowFrame

```

---

# Skeletal Mesh Naming

| Prefix | Description |
|------|------|
| SK_ | Skeletal Mesh |

Examples:

```

SK_Player
SK_WPN_AKM
SK_NPC_Police

```

---

# Material Naming

| Prefix | Description |
|------|------|
| M_ | Master Material |
| MI_ | Material Instance |

Examples:

```

M_Master_Surface
M_WPN_Metal
MI_WPN_Rust
MI_WPN_Black

```

---

# Texture Naming

| Prefix | Description |
|------|------|
| T_ | Texture |

Texture suffix rules:

| Suffix | Meaning |
|------|------|
| _D | Diffuse / Albedo |
| _N | Normal |
| _R | Roughness |
| _M | Metallic |
| _AO | Ambient Occlusion |
| _E | Emissive |

Examples:

```

T_WPN_AKM_D
T_WPN_AKM_N
T_WPN_AKM_R

```

---

# Audio Naming

| Prefix | Description |
|------|------|
| SFX_ | Sound Effect |
| MUS_ | Music |
| VO_ | Voice |

Examples:

```

SFX_WPN_AKM_Fire
SFX_WPN_Crowbar_Hit
MUS_Combat
VO_Police_Command

```

---

# Niagara / VFX Naming

| Prefix | Description |
|------|------|
| NS_ | Niagara System |
| NF_ | Niagara Function |

Examples:

```

NS_WPN_MuzzleFlash
NS_WPN_BulletImpact

```

---

# Animation Naming

| Prefix | Description |
|------|------|
| AN_ | Animation |
| AM_ | Animation Montage |

Examples:

```

AN_Player_Run
AN_Player_Idle
AM_Rifle_Reload
AM_Crowbar_Swing

```

---

# Weapon ID System

All weapons use a structured ID system.

Format:

```

[type]-[slot]-[name]

```

Example:

```

f-p-akm
f-s-makarov
m-s-crowbar
m-p-fireaxe
u-u-molotov

```

---

# Weapon Type Codes

| Code | Meaning |
|----|----|
| f | firearm |
| m | melee |
| k | knife |
| u | utility |

---

# Weapon Slot Codes

| Code | Slot |
|----|----|
| p | primary |
| s | secondary |
| k | knife |
| u | utility |

---

# Item ID System

Items follow similar structure:

```

i-[category]-[name]

```

Example:

```

i-med-bandage
i-med-medkit
i-tool-lockpick

```

---

# Faction ID System

```

fac-[name]

```

Examples:

```

fac-police
fac-raiders
fac-militia
fac-scavengers

```

---

# Location ID System

```

loc-[area]-[name]

```

Examples:

```

loc-city-alexanderplatz
loc-city-teufelsberg
loc-forest-outpost

```

---

# External Asset Naming (Blender / Source Files)

Source assets must follow clear naming.

Format:

```

category_name_version

```

Example:

```

weapon_crowbar_v01.blend
building_altbau_wall_v02.blend
prop_barrel_v01.blend

```

---

# Exported Asset Naming

Exported files (FBX / textures):

Example:

```

SM_WPN_Crowbar.fbx
SM_PROP_Barrel.fbx

```

Textures:

```

T_WPN_Crowbar_D.png
T_WPN_Crowbar_N.png

```

---

# Folder Naming Rules

Folders should follow these rules:

| Rule | Description |
|-----|-----|
| PascalCase | for UE folders |
| singular or category names | keep consistent |
| avoid deep nesting | limit folder depth |

Example:

```

Weapons/Firearms/Makarov
World/Buildings/Altbau
Characters/Player

```

---

# Naming Example (Complete Weapon)

Example crowbar weapon assets:

```

BP_WPN_Crowbar
SM_WPN_Crowbar
MI_WPN_Crowbar_Rust
T_WPN_Crowbar_D
SFX_WPN_Crowbar_Hit
DA_WPN_Crowbar

```

---

# Guiding Principle

Names should always answer:

**What is this asset and what system does it belong to?**

Good naming reduces debugging time and improves team collaboration.

