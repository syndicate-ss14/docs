# Gun Overhaul

| Designers | Coders | Implemented | GitHub Links |
|---|---|---|---|
| DVD Player, mqole | DVD Player, iaada | :x: | TBD |

## Introduction

Guns in SS14 have a medium-high barrier of entry. 

Most guns in game take specific forms of ammunition, some can toggle between different modes, have different stats, most of which are conveyed using the examine menu. However, unless the player has experience with gun terminology, there is a lot of mental overhead required to memorize all of these statistics for each individual entity. Which gun takes shotgun shells, and which gun takes .35 precision ammo? What is the difference between a Drozd and a Lecter? And why do all these guns look so similar?

To ease the learning burden, the design of guns should prioritise:
- **Glance value.** Visual designs should be distinctive and signal the gun's properties.
- **Minimal examine text.** Provide only the information that the player needs - no need to focus on the details at first blush.
- **Distinct categories.** Sorting every gun into player-facing boxes can quickly clue a player in to what to expect from how a gun handles.
- An optional **advanced stat viewer.** Keep all the numbers and details on a seperate tab so those who are interested in combat can still get into the weeds.

## Sorting Guns

Here is the proposed categorisation system for guns:

### Categories

All guns should fit into exactly one of the following **categories**, determined by the type of ammunition they accept and their general identity.

```mermaid
flowchart LR
    A(Ammunition) --> B(Handheld)
    B --> C["`**Pistol**
    Small size. Low capacity and damage, but easily concealable.`"]
    B --> D["`**Revolver**
    Heavier-hitting than a pistol, but a chore to reload.`"]
    A --> E(Precision)
    E --> F["`**Rifle**
    All-rounder with a focus on accuracy and DPS.`"]
    E --> G["`**Sniper**
    Slow rate of fire and ammo capacity, but hits hard.`"]
    A --> H(Wide Spread)
    H --> I["`**Machine Gun**
    Sacrifices accuracy in favour of a huge magazine capacity.`"]
    H --> J["`**Shotgun**
    Shoots several bullets in an arc that fans out.`"]
    K(Energy) --> L(Lethal)
    L --> M["`**Laser**
    Shoots a single beam that goes through glass walls and deals heat damage.`"]
    L --> N["`**Blaster**
    Shoots several heat projectiles in an arc that fan out.`"]
    K --> O(Non-Lethal)
    O --> P["`**Disabler**
    Deals stamina damage.`"]
    Q(Other) --> R["`**Launcher**
    Loadable with explosives. Slow fire rate.`"]
    Q --> S["`**Fuel**
    Loadable with reagents.`"]
    Q --> T["`**Special**
    Anything that doesn't fall into one of the other categories.`"]
```

### Qualities

From this base category system, each gun then has two *qualities*. Qualities should give a general overview of the gun's unique characteristics, and serve as an at-a-glance description of the gun's stats. For example:

- An Mk 58 as a *balanced*, *back-up* **pistol**
  - Generally balanced stats, but more of a sidearm than a main weapon
- A Drozd as a *rapid-fire* **machine gun**
  - Extremely fast rate of fire
- An Enforcer as a *wide-spread*, *balanced* **shotgun**
  - Balanced stats, and fans bullets out in a wide arc to increase area of effect
- A China Lake as an *aggressive*, *demolition* **launcher**
  - It's scary, and it will explode things
- A Kammerer as a *precision* **shotgun**
  - A smaller arc of bullets makes it harder to hit a target, but those bullets do more damage
- A Musket as a *precision* *haymaker* **sniper**
  - Heavy hitting ammo, and it doubles as a melee weapon

While **categories** are static identifiers that exist to denote a gun's accepted ammunition and general purpose, *qualities* are more flexible and subjective. These two systems of categorisation combine to provide a lot more glance value to guns.