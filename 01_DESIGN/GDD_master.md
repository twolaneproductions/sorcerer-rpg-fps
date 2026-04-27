# GDD_master.md
## Ashenmoor — Game Design Document (Master)
**Gate Shaker Press**
**Version:** 0.2
**Last Updated:** 2026-04-26
**Status:** Phase 0 — Draft

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Engine and Platform](#2-engine-and-platform)
3. [Genre and Tone](#3-genre-and-tone)
4. [Story Summary](#4-story-summary)
5. [Player Character](#5-player-character)
6. [Core Gameplay Loop](#6-core-gameplay-loop)
7. [Magic Weapons](#7-magic-weapons)
8. [Armor and Items](#8-armor-and-items)
9. [Key Item](#9-key-item)
10. [Enemy Roster](#10-enemy-roster)
11. [NPCs](#11-npcs)
12. [World Structure](#12-world-structure)
13. [Quest Progression](#13-quest-progression)
14. [UI and Save System](#14-ui-and-save-system)
15. [Audio and Art Direction](#15-audio-and-art-direction)
16. [Scope and Constraints](#16-scope-and-constraints)

---

## 1. Project Overview

**Ashenmoor** is a short-form first-person shooter with JRPG structural elements, built in UZDoom and set in a medieval fantasy world. Target playtime is **one hour**. The player controls a young sorcerer's apprentice investigating the disappearance of his master, moving through a small town hub, a corrupted overworld, and a demon-occupied castle toward a dramatic finale.

The game blends the fast-paced, heavy-hitting combat feel of the classic Doom engine with the NPC interaction, inventory depth, and narrative investment of a Japanese RPG while prioritizing atmosphere, tight pacing, and a memorable ending.

*See: `narrative_master.md` for full story summary.*  

---

## 2. Engine and Platform

**Engine:** UZDoom
Chosen for its first-person combat foundation, scripting depth sufficient for NPC dialogue and quest flags, and cross-platform support without licensing cost.

**Platform:** PC — Windows primary, Mac and Linux via GZDoom's native support. Initial release on itch.io.

**Performance Target:** 60fps at 1080p on mid-range hardware.

*Full technical detail in: `02_Technical/tech_overview.md`*

---

## 3. Genre and Tone

**Genre:** First-Person Shooter / JRPG Hybrid — Medieval Dark Fantasy

**Tone:** A mash of colorful JRPG fantasy and dark, gothic atmosphere. The world was recently good and is being corrupted — the evil is applied, not intrinsic, which makes it feel like a loss. Combat is fast. Narrative moments are slow. The contrast is deliberate and central to the experience.

**Primary Influences:**
- FPSs
    - *Doom* series — combat pacing, weapon feel, arena design
    - *Heretic / Hexen* — fantasy FPS aesthetic and magic weapon precedent
- JRPGs
    - Final Fantasy -- earlier entries, e.g. I-III
    - Dragon Quest series
        - particularly its art style and sense of whimsy
- Other Games
    - Castlevania series for the atmosphere of the castle/dungeon.
    - Legend of Zelda: Ocarina of Time -- dungeons.
- Other Influences
    - Vampire Hunter D (1985)
    - Dragon Ball Z: the Garlic Jr. saga
    - Gothic literature and medieval chronicle — narrative register and world texture

---

## 4. Story Summary

The player's **master** has gone north to confront the **Banished Lord** and has not returned. **King Orvyn** of **Thornwall** commissions the player to investigate and return with proof the Banished Lord has been slain. Crossing the corrupted **Wychfeld**, the player gains entry to **Ashenmoor Castle** via a drowned wizard's **wraith** and a flooded moat, fights through its interior, and descends to the deepest dungeon — where the master is discovered to have turned traitor, opening a demonic portal beside the Banished Lord. In the final confrontation, the Sorcerer will lose his head but will nonetheless close the portal and bring down the castle around him.

*Full beat-by-beat story in: `01_Design/narrative.md`*

---

## 5. Player Character

**Name:** Sorcerer
**Abilities:** Magic weapon combat, consumable item use, swimming (moat sequence), NPC dialogue
**Starting Equipment:** The Witch Switch (infinite minor wand), Apprentice's Robe, one Tincture of Mending
**Progression:** No leveling system. Power grows entirely through equipment and weapon acquisition.

---

## 6. Core Gameplay Loop

```
Explore zone
    → Combat encounters
    → Discover items and NPCs
    → Advance quest flags
    → New access granted
    → Next zone
```

Two alternating registers: **Town (slow)** — NPC dialogue, shopping, quest context. **Field and Castle (fast)** — movement, threat management, resource conservation. Each register makes the other feel more pronounced.

---

## 7. Magic Weapons

| Weapon | Doom Equivalent | Ammunition | Notes |
|---|---|---|---|
| Witch Switch | Pistol | Infinite minor mana | Starting weapon, always available |
| Scatterstaff | Shotgun | Bone Pellet Mana | Workhorse close-range weapon |
| The Tempest Rod | Chaingun | Storm Flux | Wind-up sustained fire |
| The Comet Staff | Rocket Launcher | Comet Cores | Splash damage, self-damage risk |
| The Emanation Reed (Magestream Wand) | Plasma Rifle | Arcane Plasma Vials | Rapid-fire arcane bolts |
| The Iron of Hell | BFG 9000 | Soul Confluence | Rare, devastating, saves itself for the finale |
| The Hungering Branch (Blood-Sucking Bough) | Chainsaw | None — self-fueling | Melee, converts enemy vitality to mana |

<!-- Time permitting, some bonus weapons:

| Weapon | Doom Equivalent | Ammunition |
|---|---|---|
| The Twin Wyrm | Super Shotgun | Dragonfire Essence |
| The Siege Spire (Bastion Breaker) | Ballista | Spire Bolts |
| The Eye of the Void | Unmakyr | Eternity Shards |
| The Anima Reliquary | Soul Cube | Kill-charged (5 kills) | -->

*Full weapon specs and damage values in: `01_Design/GDD_systems.md`*

---

## 8. Armor and Items

Kept deliberately lean for a one-hour game. The player finds or buys a small number of meaningful upgrades rather than managing a large inventory.

**Armor (four pieces — body, head, hands, accessory):**

| Piece | Slot | Effect |
|---|---|---|
| Apprentice's Robe | Body | Starting armor — minimal protection |
| Warded Travel Cloak | Body | Reduces physical damage — purchasable in Thornwall |
| Circlet of Warding | Head | Reduces magical disorientation effects |
| The Wizard's Own Amulet | Accessory | Given by the wraith — grows stronger as player descends |

**Consumables (five types):**

| Item | Effect | Scarcity |
|---|---|---|
| Tincture of Mending | Small health restore | Common |
| Draught of Vitality | Large health restore | Rare |
| Mana Vial | Restores moderate mana across weapons | Common |
| Ghostlight Torch | Reveals hidden enemies, illuminates darkness | Moderate |
| Sorcerer's Salve | Temporarily amplifies spell damage | Rare |

**Narrative Consumables (unique):**

| Item | Source | Effect |
|---|---|---|
| Bread and Salt | Given by rescued couple | Restores health and mana simultaneously — one only |
| Shard of the Relic | Remains after wraith summoning | Auto-activates at finale — one defensive burst |

*Full item stats and placement in: `01_Design/GDD_systems.md`*

---

## 9. Key Item

**The Relic** — A magical artifact belonging to the drowned wizard, confiscated by Father Cassian of Thornwall after the wizard was driven from town, kept in the church vestry for safekeeping. Retrieved by the player after speaking with townspeople to understand its significance.

Used to summon the Water-Wraith at the dark pool near Ashenmoor's outer ruins, granting access to the moat and the castle interior. A fragment of the relic (the Shard) persists as a consumable through the remainder of the game.

The Relic is the game's one mandatory key item. No other hard-locked progression gates exist.

*Quest integration in: `01_Design/GDD_systems.md`*

---

## 10. Enemy Roster

Enemies organized by zone of primary appearance. Behavior, health values, damage output, and drop tables detailed in the enemy design system document.

**Wychfeld:**
- Demonic Wolves — fast, silent, pack hunters
- Goblins — organized, camp-based, command hierarchy
<!-- - Lesser Wraiths — moor only, require Ghostlight Torch to fully materialize -->

**Ashenmoor Grounds and Interior:**
- Corrupted Soldiers — methodical, armored, precise
- Demonic Peasants — looping and aimless, dangerous in numbers
- Skeletons — fast, brittle, swarm behavior
- Zombies — slow, high health, dangerous at close range

**Elite / Boss:**
- Demonic Prince — elegant, blade-based, close-range energy attack
- Demonic Princess — primary caster, uses Prince as shield
- Demonic Knights — seven encountered in dungeon corridor, armored, coordinated, final gauntlet before the cell
- The Master — human sorcerer, range attacks, opening the portal
- Necromancer - demonic sorcerer, range attacks, opening the portal
- Banished Lord — finale boss, close-range attacks

*Enemy stats and behavior detail in: `01_Design/GDD_systems.md`*

---

## 11. NPCs

**Thornwall Town:**
- **Father Cassian** — holds the Relic, gives it freely, provides the most complete account of the wizard's history
- **Maret (hedge-witch)** — sells exotic consumables, hints at the wraith and the dark pool
- **Brother Oswin (apothecary)** — sells healing and mana items, speaks warmly of the wizard
- **Aldra (blacksmith)** — sells and upgrades equipment, mentions the wizard in passing
- **Hobb (tavern keeper)** — rumor hub, fragmented intelligence about the north
- **Sela and Davan** — rescued couple, give the Bread and Salt before the player departs

**Thornwall Castle:**
- **King Orvyn** — quest giver, reward promise, portrait of the wizard on his wall
- **Queen Isabeau** — silent appearance, no dialogue
- **Galen (court physician)** — gives a Tincture of Mending, speaks of the wizard fondly
- **Emmet (page)** — atmosphere and lore, most candid voice in the castle
- **Aldric** — steward, gate to king, refuses to let the apprentice enter until magic is shown
<!-- - Captain Amis — military intelligence exchange -->

**Wychfeld:**
- **Gest** — elderly farmer who refused to leave, optional wolf intelligence and errand

*Full dialogue scripts in: `01_Design/npcs_and_dialogue.md`*

---

## 12. World Structure

Linear with one optional branch. The moat is a one-way threshold — the player cannot return to Thornwall or the Wychfeld once they enter Ashenmoor.

```
Tutorial Woods
    └── Thornwall (hub)
            └── Thornwall Castle (one visit)
                    └── Wychfeld
                            ├── Amber Fields [Gest — optional errand]
                            ├── Greywood
                            <!-- [optional: Watchtower]
                            ├── Blighted Moor [optional: Sunken Abbey] -->
                            └── Ashenmoor Approach
                                    └── Outer Ruins / Dark Pool
                                            └── Moat [one-way threshold]
                                                    └── Barbican
                                                            └── Courtyard
                                                                    └── Great Hall
                                                                            └── Chambers
                                                                                    └── Dungeons
                                                                                            └── Deepest Cell (finale)
```

*Room-by-room level detail in: `01_Design/levels.md`*

---

## 13. Quest Progression

Flag-based rather than journal-based. The world responds to what the player has done. No explicit task list is shown — context is gathered through NPC conversation.

**Main Quest Spine:**
1. Rescue the couple — tutorial, automatic
2. Enter Thornwall, speak with NPCs
3. Access Thornwall Castle, receive quest from King Orvyn
4. Retrieve the Relic from Father Caelan
5. Cross the Wychfeld
6. Summon the wraith at the dark pool, enter the moat
7. Clear Ashenmoor — barbican, courtyard, hall, chambers, dungeons
8. Confront the finale

**Optional Quest Content:**
- Gest's errand (Amber Fields)
<!-- - Sunken Abbey exploration (Blighted Moor)
- Watchtower clearance and view (Greywood) -->
- Full NPC conversation trees in Thornwall

---

## 14. UI and Save System

**HUD:** Health indicator, active weapon mana, active consumable slot. Minimal — nothing that breaks the gothic atmosphere.

*?Inventory access pauses gameplay — a deliberate JRPG-mode moment within the FPS flow, reinforcing the genre hybrid identity.?*

*Full UI specifications and HUD layout in: `GDD_ui_and_hud.md`*
*Full inventory system mechanics in: `GDD_inventory_system.md`*

---

## 17. Save System

The game saves at defined checkpoints rather than freely, reminiscent of classic JRPGs, typically by resting (at an inn) or praying. Primary save points are:

- Thornwall
    - Church
    - Inn (also replenishes health/mana)
- The Woodcutter's Chapel (Greywood)
- Ashenmoor Chapel

No manual save outside of these points. The design intent is that resource scarcity and checkpoint spacing create meaningful tension without punishing the player excessively.

*Full save architecture in: `GDD_save_system.md`*

---

## 18. Audio Direction

The game's sonic landscape moves from warmth to dread as the player progresses north. Thornwall is fire and conversation and distant music. The Wychfeld is wind, silence, and wrong animal sounds. Ashenmoor is fire in the wrong colors and the growing Latin choral drone that guides the player downward through the dungeon.

**Soundtrack**

Largely Dungeon Synth inspired.

In the final dungeon, the Deepest Cell, a **Latin choir** rings in the final boss, beginning as recognizable liturgical fragments and becoming increasingly distorted and non-liturgical as the player descends, functioning simultaneously as navigation tool and atmospheric escalation device.

*Full audio direction and SFX list in: `audio_direction_document.md` and `audio_sfx_list.md`*

---

## 19. Art Direction

Medieval fantasy with gothic architecture and corrupted natural environments. The visual contrast between Thornwall (warm, maintained, human) and Ashenmoor (ashen, geometric, wrong) is the game's primary visual argument. The Wychfeld sits between them tonally — natural forms beginning to distort, farmland going grey, forest light going green.

The player's sorcerer aesthetic draws from apprentice-scholar rather than warrior — robes, not armor; wands and staves, not swords. The magical weapons should read as elegant, carved, mystical objects.

*Full direction in: `03_Art/art_direction.md` and `04_Audio/audio_direction.md`*

---

## 16. Scope and Constraints

**Target playtime:** One hour
**Team size:** Two people
**Budget:** Minimal — no licensed assets, no voice acting, no external contractors in initial scope

**In scope:**
- Complete main quest spine
- Seven weapons
- Four armor pieces, five consumable types, two narrative consumables
- All named NPCs and core dialogue
- All main levels plus Amber Fields optional content

**Cut from larger design — available for post-launch update if desired:**
- Blighted Moor and Sunken Abbey (optional zone)
- Twin Wyrm, Siege Spire, Unraveling Eye, Anima Vessel weapons
- Additional armor pieces
- Covered portrait mystery in Thornwall Castle throne room
- Watchtower reduced to environmental landmark only

*Living cut list in: `00_Admin/cut_list.md`*

---

*Sub-documents are authoritative over this master when conflicts arise. Flag conflicts at the next team sync.*