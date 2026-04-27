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

The player controls **Sorcerer**, a young apprentice whose master has gone north to the kingdom of **Thornwall** to answer the call of **King Orvyn** and has not returned. Confronting Orvyn, the Sorcerer learns that his master was commissioned to head further North, across the corrupted **Wychfeld** forest, to gain secret entry to **Ashenmoor Castle** and confront the **Banished Lord**.

The Sorcerer will trace his master's footsteps, befriending a drowned wizard's wraith who will transport him to Ashenmoor's moat, allowing him to fight his way into the castle, progressing through darker interior zones toward the castle's deepest dungeon.

There he discovers his master has allied himself with the Banished Lord to open a demonic portal. In the final confrontation, the Sorcerer will lose his head, but nonetheless he will close the portal and bring down the castle around him.

*Full beat-by-beat story in: `narrative_story_beats.md`*

---

## 5. Player Character

**Name:** Sorcerer (player-facing title; internal name negotiable)
**Role:** Apprentice mage, sole protagonist
**Abilities:** Magic weapon combat, consumable item use, swimming (moat sequence), NPC dialogue interaction
**Starting Equipment:** The Witch Switch (infinite minor wand), Apprentice's Robe, Apprentice's Cap, one Tincture of Mending
**Progression:** Health increases, if not through XP leveling up, perhaps via "heart container" items, a la Legend of Zelda. Power growth through equipment acquisition -- better wands, robes, and armor found or purchased throughout the game.

*Full character bible in: `narrative_character_bibles/char_sorcerer.md`*

---

## 6. Core Gameplay Loop

```
Explore zone
    → Encounter enemies (combat)
    → Defeat enemies (drops, zone clearance)
    → Discover items, lore, NPCs
    → Advance quest flags
    → Return to hub (Thornwall) or press forward
    → New zone unlocked or deeper access granted
```

The loop has two registers: **town (slow)** and **field/castle (fast)**. Town is JRPG-mode — NPC dialogue, shopping, quest pickup, atmosphere. Field and castle are Doom-mode — movement, positioning, threat management, resource conservation. The game alternates between these registers deliberately, using each to make the other feel more pronounced.

---

## 7. Combat System

Fast, fluid first-person combat native to UZDoom's movement model. The player has a basic melee attack, but combat is overwhelmingly magic-based ranged combat using the wand arsenal.

**Key combat parameters:**
- Player movement speed — fast, Doom-adjacent, not realistic
- No regenerating health — health pickups and consumables only
- Mana shared across weapons via individual ammunition pools
- Enemy strength scales with zone depth -- the deeper into the forest, the deeper into the castle, the more lethal enemies become

*Full combat detail in: `GDD_combat_systems.md`*

---

## 8. Magic Weapons

Twelve wands and staves, each corresponding to a landmark weapon from the Doom series translated into a medieval fantasy magic equivalent. Weapons vary by damage type, fire rate, ammunition type and scarcity, and special mechanical behavior.

| Weapon | Doom Equivalent | Ammunition |
|---|---|---|
| The Witch Switch | Pistol | Infinite minor mana |
| Scatterstaff | Shotgun | Bone Pellet Mana |
| The Twin Wyrm | Super Shotgun | Dragonfire Essence |
| The Tempest Rod | Chaingun | Storm Flux |
| The Comet Staff | Rocket Launcher | Comet Cores |
| The Emanation Reed (Magestream Wand) | Plasma Rifle | Arcane Plasma Vials |
| The Iron of Hell | BFG 9000 | Soul Confluence |
| The Hungering Branch (Blood-Sucking Bough) | Chainsaw | None — self-fueling |
| The Siege Spire (Bastion Breaker) | Ballista | Spire Bolts |
| The Eye of the Void | Unmakyr | Eternity Shards |
| The Anima Reliquary | Soul Cube | Kill-charged (5 kills) |

*Full weapon specs, damage values, and fire rates in: `GDD_magic_weapons.md`*

---

## 9. Armor System

Twelve armor pieces across five slots — body, head, hands, feet, and accessory. The player begins in minimal apprentice gear and progressively acquires magical protections. No piece is purely cosmetic — each carries a mechanical effect.

Two late-game pieces (The Dead Wizard's Robe and The Wizard's Own Amulet) are connected narratively and carry a combined bonus when worn together.

**Slots:** Body / Head / Hands / Feet / Accessory

*Full armor stats and acquisition locations in: `GDD_armor_and_items.md`*

---

## 10. Items and Consumables

Twelve consumable items across four categories: healing, mana restoration, utility, and magical augmentation. Items are found in the environment, purchased in Thornwall, and dropped by enemies. Scarcity increases with zone depth.

**Categories:**
- **Healing** — Tincture of Mending, Draught of Vitality, Bloodmoss Compress
- **Mana** — Mana Vial, Concentrated Essence
- **Utility** — Ghostlight Torch, Ward Stone, Smoke of Confusion
- **Augmentation** — Sorcerer's Salve, Ring of the Nimble
- **Narrative Consumables** — Bread and Salt (unique, one only), Shard of the Relic (activates automatically at finale)

*Full item stats and locations in: `GDD_armor_and_items.md`*

---

## 11. Key Items

Non-consumable items that drive quest progression.

**The Relic** — A magical artifact belonging to the drowned wizard, confiscated by Father Cassian of Thornwall after the wizard was driven from town, kept in the church vestry for safekeeping. Retrieved by the player after speaking with townspeople to understand its significance. Used to summon the Water-Wraith at the dark pool near Ashenmoor's outer ruins, granting access to the moat and the castle interior. A fragment of the relic (the Shard) persists as a consumable through the remainder of the game.

*Quest integration detail in: `GDD_quest_system.md`*

---

## 12. Enemy Roster

Enemies organized by zone of primary appearance. Behavior, health values, damage output, and drop tables detailed in the enemy design system document.

**Wychfeld — Exterior**
- Demonic Wolves — fast, silent, pack hunters
- Goblins — organized, camp-based, command hierarchy
- Lesser Wraiths — moor only, require Ghostlight Torch to fully materialize

**Ashenmoor — Castle Grounds**
- Corrupted Soldiers — methodical, precision movement, heavily armored
- Demonic Peasants — looping, aimless, dangerous in numbers

**Ashenmoor — Interior**
- Skeletons — fast, brittle, swarm behavior
- Zombies — slow, high health, dangerous at close range
<!-- - Various Monsters — mid-tier castle enemies, zone-specific variants -->

**Ashenmoor — Elite**
- Demonic Knights — seven encountered in dungeon corridor, armored, coordinated
- Demonic Prince — elegant, blade-based, close-range energy attack
- Demonic Princess — primary caster, uses Prince as shield

**Ashenmoor - Dungeon**
- The Master — human sorcerer, range attacks, opening the portal
- Necromancer - demonic sorcerer, range attacks, opening the portal
- Banished Lord — finale boss, close-range attacks

*Full enemy specs in: `systems_enemy_design.md`*

---

## 13. NPCs and Dialogue

NPCs are concentrated in Thornwall town and Thornwall Castle. The overworld contains one significant NPC (Gest). Ashenmoor contains one ghostly NPC to deliver a hint at a secret.

**Thornwall Town**
- Aldra — blacksmith, equipment upgrades
- Brother Oswin — apothecary, healing and mana items
- Maret — hedge-witch, exotic consumables and hints
- Father Cassian — church, keeper of the Relic
- Hobb — tavern keeper, rumor hub
- Tomlin — cartwright, general supplies
- Sela and Davan — rescued couple, Bread and Salt gift

**Thornwall Castle**
- King Orvyn — quest giver, reward promise
- Aldric — steward, gate to king
- Captain Amis — military intelligence exchange
- Galen — court physician, healing item gift
- Emmet — young page, lore and atmosphere
- Queen Isabeau — silent appearance, no dialogue

**Wychfeld**
- Gest — elderly farmer, wolf intelligence, optional errand

*Full dialogue scripts in: `narrative_dialogue_scripts/`*
*Character bibles in: `narrative_character_bibles/`*
*Dialogue system mechanics in: `GDD_npc_and_dialogue_systems.md`*

---

## 14. Quest System

Quest progression is flag-based rather than journal-based — the world responds to what the player has done rather than presenting an explicit task list.

Speaking to NPCs should provide sufficient context for players to proceed.

Players who rush will miss texture but will not be hard-blocked except at the Relic acquisition, which is a required step.

**Main Quest Spine:**
1. Rescue the couple (tutorial — automatic)
2. Enter Thornwall
3. Gain access to Thornwall Castle
4. Receive quest from King Orvyn
5. Equip in town
6. Gather Relic from Father Cassian
7. Cross the Wychfeld
8. Summon the wraith, enter the moat
9. Clear Ashenmoor
10. Confront the finale

**Optional Quest Content:**
- Gest's errand (Amber Fields)
- Sunken Abbey exploration (Blighted Moor)
- Watchtower clearance and view (Greywood)
- Full NPC conversation trees in Thornwall

*Full quest flag architecture in: `GDD_quest_system.md`*

---

## 15. World Structure and Levels

The game world is linear with optional branching. The player cannot return to earlier zones once certain thresholds are crossed (moat entry is one-way).

```
Tutorial Woods
    └── Thornwall (hub — full NPC access)
            └── Thornwall Castle (one visit)
                    └── Wychfeld Overworld
                            ├── Amber Fields
                            ├── Greywood [optional: Watchtower]
                            ├── Blighted Moor [optional: Sunken Abbey]
                            └── Ashenmoor Approach
                                    └── Outer Ruins / Dark Pool
                                            └── Moat (one-way threshold)
                                                    └── Barbican
                                                            └── Courtyard
                                                                    └── Great Hall
                                                                            └── Chambers
                                                                                    └── Dungeons
                                                                                            └── Deepest Cell (finale)
```

*Individual level documents in: `01_Design/Levels/`*

---

## 16. Inventory and UI

The player carries weapons, armor (equipped across five slots), and consumable items in a menu-accessible inventory screen. The HUD displays current health, current mana for the active weapon, equipped armor summary, and active consumable slot.

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

*Full art direction and style references in: `art_direction_document.md`*

---

## 20. Scope and Cut List Reference

The following elements are in full scope for the initial release:

- Complete main quest spine
- All twelve weapons
- All twelve armor pieces
- All twelve consumable items
- All named NPCs and their dialogue trees
- All main and optional levels

The following elements are candidates for the cut list if schedule pressure requires:

- Voice acting (replaceable with text-only dialogue)
- The Blighted Moor and Sunken Abbey (optional zone, cuttable without breaking main quest)
- The Anima Vessel weapon (mechanically complex, deprioritize if implementation is costly)
- Secondary portrait mystery (covered portrait in Thornwall Castle throne room — can remain unresolved as atmosphere rather than developed as content)

*Living cut list maintained in: `00_Admin/cut_list.md`*

---

*This document is a master index. All mechanical specifications, full dialogue, level layouts, and technical architecture live in their respective sub-documents referenced throughout. When this document and a sub-document conflict, the sub-document is authoritative. Flag conflicts for resolution in the next team sync.*
