# GDD_systems.md
## Ashenmoor — Game Systems Design
**OUR NEW INDIE GAME STUDIO**
**Version:** 0.1
**Last Updated:** 2026-04-26
**Status:** Phase 0 — Draft

---

## Table of Contents

1. [Combat System](#1-combat-system)
2. [Magic Weapons](#2-magic-weapons)
3. [Armor System](#3-armor-system)
4. [Consumable Items](#4-consumable-items)
5. [Key Item](#5-key-item)
6. [Enemy Roster](#6-enemy-roster)
7. [NPC and Dialogue System](#7-npc-and-dialogue-system)
8. [Quest Flag System](#8-quest-flag-system)
9. [Shop System](#9-shop-system)
10. [Inventory and UI](#10-inventory-and-ui)
11. [Save System](#11-save-system)
12. [Moat Swim Sequence](#12-moat-swim-sequence)

---

## 1. Combat System

### Overview

Combat is first-person, movement-based, and entirely magic-ranged with one melee exception (The Hungering Branch). The player survives through positioning and movement, not through a cover system or regenerating health. UZDoom's native movement model is used without significant modification — fast, fluid, Doom-adjacent.

### Player Stats

| Stat | Base Value | Notes |
|---|---|---|
| Health | 100 | Does not regenerate passively |
| Max Health | 100 | Cannot be exceeded by pickups in base design |
| Movement Speed | Standard UZDoom default | Not modified |
| Air Supply (moat) | 30 seconds | See Section 12 |

### Damage Model

All damage values are expressed as a percentage of base player health (100). This makes tuning relative and readable.

- **Light hit** — 5–10% — glancing contact, weak enemy attacks
- **Standard hit** — 15–20% — typical enemy attack, well-placed player contact
- **Heavy hit** — 25–35% — elite enemy attacks, explosive splash
- **Lethal** — 100% — the Knight Lord's beheading (scripted, not combat damage)

### Player Death

Standard UZDoom death state. Loads from the most recent autosave checkpoint. No lives system. No death penalty beyond lost progress since last checkpoint.

**Exception — the finale beheading:** This is a scripted death, not a combat death. The game does not reload. The resurrection sequence plays automatically. See Section 6 (Knight Lord) and the narrative document for full sequence detail.

### Difficulty

One difficulty setting for initial release. The game is tuned to be challenging but completable in one hour for a player of moderate FPS experience. Enemy health and damage values below are for this single difficulty. A difficulty selection system is a post-launch candidate.

---

## 2. Magic Weapons

### General Rules

- The player can carry all weapons simultaneously
- Weapons are switched instantly — no draw animation delay in base implementation
- Each weapon has its own ammunition pool — running out of ammo on one weapon does not affect others
- The Witch Switch never runs out of ammunition and is always available as a fallback
- Ammunition is found as pickups in the environment and dropped by certain enemies
- The inventory screen shows current ammo count for each weapon

### Weapon Specifications

---

#### Witch Switch
**Doom equivalent:** Pistol
**Description:** An uncarved apprentice's wand. A stick that happens to work. The player's starting weapon and permanent fallback.
**Ammunition:** Infinite minor mana — no pickup required
**Fire rate:** 1 bolt per 0.8 seconds
**Damage per shot:** 8%
**Range:** Full — no falloff
**Special mechanic:** None
**Acquisition:** Starting equipment
**Notes:** Never impressive. Never useless. The weapon the player returns to when everything else runs dry.

---

#### Scatterstaff
**Doom equivalent:** Shotgun
**Description:** A wide-mouthed, gnarled staff that fires a cone of bone-white magical pellets. Devastating at close range, diffuse at distance.
**Ammunition:** Bone Pellet Mana
**Ammo capacity:** 40 pellet-charges
**Ammo per shot:** 8 pellets fired per shot, costs 1 charge
**Fire rate:** 1 shot per 1.2 seconds (pump-equivalent pause)
**Damage per shot:** 5% per pellet × 8 pellets = up to 40% at point-blank, falling off sharply beyond mid-range
**Range:** Short to mid — significant spread
**Special mechanic:** None
**Acquisition:** Purchasable from Aldra (blacksmith) in Thornwall, or found in the Greywood
**Notes:** The workhorse. Most common ammunition type in the game.

---

#### The Tempest Rod
**Doom equivalent:** Chaingun
**Description:** A spinning, gyroscopic wand that must spool up before firing. Once spooled, it releases a sustained torrent of lightning micro-bolts.
**Ammunition:** Storm Flux
**Ammo capacity:** 200 flux-charges
**Ammo per shot:** 4 charges per second while firing
**Fire rate:** 0.1 seconds per bolt after spool-up (10 bolts/second sustained)
**Spool-up time:** 1.5 seconds from trigger to first bolt
**Damage per bolt:** 4%
**Range:** Full — no falloff
**Special mechanic:** Spool-up delay. If the player releases the trigger before firing, the spool resets. The weapon rewards commitment.
**Acquisition:** Found in a locked chest in the Ashenmoor barbican
**Notes:** Drains ammunition fast. Devastating against large groups in open spaces.

---

#### The Comet Staff
**Doom equivalent:** Rocket Launcher
**Description:** A long staff that fires a slow-moving sphere of compressed elemental force, detonating on impact with a burst of fire and shockwave.
**Ammunition:** Comet Cores
**Ammo capacity:** 12 cores
**Ammo per shot:** 1 core
**Fire rate:** 1 shot per 1.5 seconds
**Projectile speed:** Slow — approximately 40% of Witch Switch bolt speed
**Damage on impact:** 35% direct
**Splash damage:** 15% at inner radius, 8% at outer radius
**Self-damage:** Yes — firing at close range damages the player. Splash radius identical to enemy splash.
**Range:** Full — no falloff on projectile, but slow speed makes long range impractical
**Special mechanic:** Splash damage and self-damage. The player must maintain distance to use safely.
**Acquisition:** Found in the Ashenmoor courtyard, near the sealed well
**Notes:** Comet Cores are scarce. Every shot is a decision.

---

#### The Magestream Wand
**Doom equivalent:** Plasma Rifle
**Description:** A slender, precise wand that fires rapid bolts of raw violet arcane plasma in a sustained stream.
**Ammunition:** Arcane Plasma Vials
**Ammo capacity:** 150 vial-charges
**Ammo per shot:** 2 charges per bolt
**Fire rate:** 0.12 seconds per bolt (approximately 8 bolts/second)
**Damage per bolt:** 7%
**Range:** Full — slight homing on each bolt, not enough to guarantee hits but enough to assist
**Special mechanic:** Slight bolt homing — each bolt curves mildly toward the nearest enemy in its forward arc. Not reliable enough to substitute for aim but noticeably forgiving.
**Acquisition:** Found in the Ashenmoor great hall, behind the feast table
**Notes:** The feel weapon. Filling the air with violet bolts is intrinsically satisfying and intentionally so.

---

#### The Obliterator Stave
**Doom equivalent:** BFG 9000
**Description:** A massive two-handed obsidian staff with a pulsing green eye at its crown. Charges for two seconds before releasing a sphere of necrotic force that rolls through the room, spawning tendrils of death on everything it passes.
**Ammunition:** Soul Confluence
**Ammo capacity:** 3 confluences
**Ammo per shot:** 1 confluence
**Charge time:** 2 full seconds — player movement slowed during charge
**Damage — direct sphere contact:** 80%
**Damage — tendrils:** 30% per tendril, up to 3 tendrils per enemy in range
**Range:** The sphere travels forward at medium speed for the full room length before dissipating
**Special mechanic:** Charge time with movement penalty. Tendrils — every enemy within a wide radius of the sphere's path takes tendril hits regardless of line of sight. The weapon clears rooms, not targets.
**Acquisition:** One confluence found in the Ashenmoor chambers (post-Prince and Princess encounter). Two more found in the dungeon corridor approach.
**Notes:** Soul Confluence is the rarest ammunition in the game. The player will save it and then panic-fire it at the wrong moment. This is correct behavior and should be designed for.

---

#### The Hungering Branch
**Doom equivalent:** Chainsaw
**Description:** A twisted, living-wood wand covered in thorns that, when pressed against an enemy, endlessly feeds on their life force, converting it directly into mana for other weapons.
**Ammunition:** None — self-fueling
**Fire rate:** Continuous contact — approximately 20% damage per second to target
**Damage:** 20% per second (contact maintained)
**Range:** Melee only — zero standoff distance
**Special mechanic:** Mana conversion. For every 1% of health drained from an enemy, 2 charges of a randomly selected weapon's ammunition are restored. Against a standard enemy the Branch effectively refuels the player's entire arsenal if contact can be maintained.
**Acquisition:** Given by Maret (hedge-witch) in Thornwall as a parting gift if the player has completed her full conversation tree
**Notes:** Getting close enough to use it is the cost. Against standard enemies this is manageable. Against elites it is a significant risk-reward calculation.

---

### Weapon Acquisition Summary

| Weapon | Where Found | Missable? |
|---|---|---|
| Witch Switch | Starting equipment | No |
| Scatterstaff | Thornwall (purchasable) or Greywood (pickup) | No |
| The Hungering Branch | Thornwall — Maret, full conversation required | Yes — requires dialogue completion |
| The Tempest Rod | Ashenmoor barbican — locked chest | No |
| The Comet Staff | Ashenmoor courtyard — near sealed well | No |
| The Magestream Wand | Ashenmoor great hall — behind feast table | No |
| The Obliterator Stave | Ashenmoor chambers onwards | No |

---

## 3. Armor System

### Overview

Four armor slots: Body, Head, Hands, Accessory. The player begins with minimal apprentice gear. Upgrades are found or purchased. Armor is equipped from the inventory screen and takes effect immediately. There is no weight system — armor has no movement penalty.

### Armor Specifications

---

#### Apprentice's Robe
**Slot:** Body
**Protection:** 0% damage reduction — cosmetic only
**Special effect:** None
**Acquisition:** Starting equipment
**Notes:** The baseline. Everything is an upgrade from here.

---

#### Warded Travel Cloak
**Slot:** Body (replaces Apprentice's Robe)
**Protection:** 15% reduction to all physical damage (enemy melee and projectile impacts, not magical)
**Special effect:** None
**Acquisition:** Purchasable from Aldra (blacksmith) in Thornwall — 1 standard currency unit
**Notes:** The most important early purchase. Physical damage is the dominant threat in the Wychfeld.

---

#### Circlet of Warding
**Slot:** Head
**Protection:** 10% reduction to magical damage
**Special effect:** Reduces duration of disorientation effects by 50%. Disorientation occurs in the moat sequence and from the Demonic Princess's specific attacks.
**Acquisition:** Found in the Sunken Abbey — *currently on cut list.* Interim placement: found in a locked side room in the Ashenmoor barbican.
**Notes:** The moat sequence is the primary reason to acquire this before entering Ashenmoor.

---

#### The Wizard's Own Amulet
**Slot:** Accessory
**Protection:** Passive magical ward — absorbs the first 15% of any single magical hit, then recharges over 20 seconds
**Special effect:** The ward strength increases as the player descends through Ashenmoor. By the dungeon, the absorbed threshold reaches 25%. This is implemented as a zone-triggered stat change, not a player-controlled upgrade.
**Acquisition:** Given by the Water-Wraith after the summoning at the dark pool — pressed into the player's hand before they are drawn into the moat
**Notes:** The ward recharge timing means it is most useful against spaced magical attacks. Against the Demonic Princess's sustained casting it will fire once and then be unavailable. Player positioning and timing are required to maximize it.

---

### Armor Summary Table

| Piece | Slot | Physical Reduction | Magic Reduction | Special |
|---|---|---|---|---|
| Apprentice's Robe | Body | 0% | 0% | None |
| Warded Travel Cloak | Body | 15% | 0% | None |
| Circlet of Warding | Head | 0% | 10% | -50% disorientation duration |
| Wizard's Own Amulet | Accessory | 0% | Absorb 15–25% first hit | Recharges per 20s |

---

## 4. Consumable Items

### General Rules

- Consumables are used from the active consumable slot via a dedicated use key
- The active slot cycles through carried consumables
- Most consumables take effect instantly on use
- No animation delay on consumable use — the player does not lower their weapon
- Consumables stack to a maximum of 5 per type unless noted otherwise

### Standard Consumables

---

#### Tincture of Mending
**Effect:** Restores 25% health instantly
**Stack limit:** 5
**Scarcity:** Common — found throughout all zones, sold by Brother Oswin in Thornwall
**Thornwall price:** 1 currency unit
**Notes:** The primary healing item. Players should never be completely out of Tincts if they are exploring thoroughly.

---

#### Draught of Vitality
**Effect:** Restores 75% health instantly
**Stack limit:** 3
**Scarcity:** Rare — found only in significant locations (post-boss rooms, hidden side areas)
**Thornwall price:** Not sold — found only
**Notes:** Saved for emergencies. The player should feel reluctant to use one and relieved when they do.

---

#### Mana Vial
**Effect:** Restores 30 ammunition charges to every weapon simultaneously
**Stack limit:** 5
**Scarcity:** Common — found throughout all zones, sold by Brother Oswin in Thornwall
**Thornwall price:** 1 currency unit
**Notes:** The 30-charge restore is meaningful for the Tempest Rod and Magestream Wand, minimal for the Comet Staff and Obliterator Stave. For scarce-ammo weapons, a targeted Concentrated Essence is more efficient.

---

#### Ghostlight Torch
**Effect:** For 30 seconds — illuminates a wide radius around the player, reveals any hidden or partially-incorporeal enemies within the radius, and applies a 20% damage bonus to revealed enemies
**Stack limit:** 3
**Scarcity:** Moderate — found in darker interior zones, sold by Maret (hedge-witch) in Thornwall
**Thornwall price:** 2 currency units
**Notes:** The Circlet of Warding's disorientation reduction and the Ghostlight Torch's reveal mechanic are the two systems most dependent on the dungeon's darkness. Both must be playtested against the final lighting levels to confirm they are mechanically meaningful.

---

#### Sorcerer's Salve
**Effect:** For 20 seconds — all spell damage increased by 30%
**Stack limit:** 3
**Scarcity:** Rare — found in elite enemy drop tables and hidden caches
**Thornwall price:** Not sold — found only
**Notes:** Saved for the Demonic Prince and Princess encounter and the dungeon corridor. Communicating to the player that the Salve exists before they need it requires at least one pickup in the Greywood or early Ashenmoor.

---

### Narrative Consumables

These items are unique — one exists in the entire game. They cannot be purchased or found as pickups.

---

#### Bread and Salt
**Effect:** Restores 40% health and 20 charges to every weapon simultaneously
**Stack limit:** 1 (unique)
**Source:** Given by Sela and Davan (the rescued couple) when the player finds them in Thornwall before departing
**Notes:** The only item in the game that heals health and mana simultaneously. Its value is not primarily mechanical — it is the couple's only way of helping, offered without ceremony. Players who rush through Thornwall without finding the couple will not receive it. It is not missable in the sense that the couple is not hidden, but it requires the player to seek them out.

---

#### Shard of the Relic
**Effect:** Auto-activates at the start of the finale sequence in the deepest cell — absorbs the first 50% damage from any source for 10 seconds before shattering
**Stack limit:** 1 (unique)
**Source:** Remains in the player's inventory after the Relic is used to summon the wraith at the dark pool. The Relic shatters on use — the Shard is what remains.
**Notes:** The player carries this through the entire castle without being able to use it deliberately. It activates on its own when it is needed. This should be communicated to the player — either through Maret's dialogue in Thornwall (*something of his will know when the time comes*) or through a brief inventory description on the Shard itself.

---

### Consumable Summary Table

| Item | Effect | Health | Mana | Scarcity | Source |
|---|---|---|---|---|---|
| Tincture of Mending | Instant heal | +25% | — | Common | Found / Oswin |
| Draught of Vitality | Instant heal | +75% | — | Rare | Found only |
| Mana Vial | Mana restore | — | +30 all | Common | Found / Oswin |
| Ghostlight Torch | Reveal + damage | — | — | Moderate | Found / Maret |
| Sorcerer's Salve | Damage boost ×1.3 / 20s | — | — | Rare | Found only |
| Bread and Salt | Dual restore | +40% | +20 all | Unique | Sela and Davan |
| Shard of the Relic | Auto-absorb 50% / 10s | — | — | Unique | Relic aftermath |

---

## 5. Key Item

### The Relic

**Description:** A small carved artifact — material and form to be determined by art direction, but clearly magical in origin and clearly old. It hums faintly when held. Its specific function is not apparent to the player until Maret or Father Cassian provides context.

**Acquisition:** Father Cassian's vestry, Thornwall church. Given freely once the player's purpose is established through conversation.

**Function:** When brought to the dark pool at Ashenmoor's outer ruins and held over the water, it summons the Water-Wraith — the drowned wizard whose artifact it was. The Wraith surfaces, recognizes his property, and draws the player into the moat as passage into the castle. The Relic shatters on the pool's surface as the player is pulled under. The Shard remains.

**Quest flag:** `RELIC_ACQUIRED` set on pickup. `WRAITH_SUMMONED` set on use at the pool. Both flags are checked by the level transition into the moat sequence — the player cannot enter the moat without `WRAITH_SUMMONED` being true.

**Inventory behavior:** Displayed as a key item, not a consumable. Cannot be dropped or used from the consumable slot. Disappears from inventory after use at the pool, replaced by the Shard.

---

## 6. Enemy Roster

### General Rules

- All enemy health expressed as a percentage of player base health (100) for relative readability
- All enemy damage expressed as a percentage of player base health
- Enemy behavior uses UZDoom's native AI state machine (patrol → detect → attack → death) with ZScript modifications where noted
- No enemy respawns after death — zones are permanently cleared

---

### Wychfeld Enemies

#### Demonic Wolf
**Health:** 30%
**Movement:** Fast — approximately 150% of player speed
**Attack:** Bite — 15% damage, melee range only
**Behavior:** Pack hunting. Individual wolves circle at range before committing. Attack in coordinated rushes when three or more are present. Never attack alone if pack is available.
**Detection:** Sound and sight — significantly longer detection range than standard enemies. Silent movement — the player receives no audio warning before the wolf is close.
**Drop:** Small chance of Bone Pellet Mana (Scatterstaff ammo)
**Notes:** The silence is the primary threat. The Scatterstaff is the ideal response — wide spread compensates for the wolf's fast movement.

---

#### Goblin
**Health:** 45%
**Movement:** Standard
**Attack:** Thrown rock — 10% damage, mid-range. Crude blade — 18% damage, melee.
**Behavior:** Camp-based. Goblins patrol defined areas around their camps and do not pursue beyond their patrol boundary except when a commander is present. Commanders (larger goblins, one per camp) extend the entire camp's pursuit range and increase attack frequency while alive. Killing the commander first is the correct tactical approach.
**Detection:** Sight only — the player can approach camps from outside the sightline safely
**Drop:** Small chance of Storm Flux (Tempest Rod ammo)
**Notes:** The command hierarchy requires the player to identify the commander before engaging. Commander goblins wear slightly different headgear — communicate this clearly through art.

---

### Ashenmoor Ground and Interior Enemies

#### Corrupted Soldier
**Health:** 60%
**Movement:** Standard — slightly slower than player
**Attack:** Blade — 22% damage, melee. Shield bash — 12% damage, melee, brief stagger on hit.
**Behavior:** Methodical. Soldiers advance in formation where possible, maintaining spacing between each other. They do not rush. The shield bash interrupts the player's casting briefly (0.5 second interrupt on hit) — this is the mechanic that makes them dangerous.
**Detection:** Sight and sound
**Drop:** Moderate chance of Arcane Plasma Vials (Magestream ammo)
**Notes:** The cast interrupt is the primary threat. Fighting multiple soldiers simultaneously is punishing. Draw them apart where possible.

---

#### Demonic Peasant
**Health:** 35%
**Movement:** Standard, slightly erratic
**Attack:** Scratch — 8% damage, melee. Occasional thrown object — 6% damage, short range.
**Behavior:** Looping patrol patterns, aimless until alerted. Once alerted, they charge directly at the player without tactical consideration. Dangerous only in numbers — individually they are minor threats.
**Detection:** Sight only — easily avoided if the player is observant
**Drop:** Small chance of Bone Pellet Mana
**Notes:** The courtyard and great hall are the primary demonic peasant zones. The feast sequence in the hall features the highest density. The Scatterstaff clears them efficiently.

---

#### Skeleton
**Health:** 25%
**Movement:** Fast — 130% of player speed
**Attack:** Claw — 12% damage, melee
**Behavior:** Swarm. Skeletons operate in groups of 4–8 and engage simultaneously. Individually fragile, collectively disorienting.
**Detection:** Sight
**Drop:** Small chance of Storm Flux
**Notes:** The Tempest Rod is the intended counter — its sustained fire handles swarms efficiently once spooled. The Scatterstaff is effective at close range but the reload pause is dangerous when surrounded.

---

#### Zombie
**Health:** 80%
**Movement:** Slow — 60% of player speed
**Attack:** Grab — 25% damage, melee, brief movement lock on hit
**Behavior:** Direct pursuit. No tactics. Absorbs significant damage before falling.
**Detection:** Sight and sound — long detection range
**Drop:** Moderate chance of Tincture of Mending
**Notes:** The movement lock on the grab attack is the primary danger. The Comet Staff's splash damage is efficient against zombies due to their slow movement — they cannot evade a slow projectile. The Magestream Wand's sustained damage output is also effective.

---

### Elite Enemies

#### Demonic Prince
**Health:** 150%
**Movement:** Fast and precise — 120% of player speed, changes direction smoothly
**Attacks:**
- Long blade — 28% damage, melee, wide arc
- Dark energy bolt — 20% damage, short range, fires when cornered or at low health
**Behavior:** The Prince is the Princess's shield. He positions himself between the Princess and the player at all times. He prioritizes intercepting projectiles and absorbing hits over dealing damage himself. His own attacks are reactive — he strikes when the player gets close to the Princess or when he has a clear opening.
**Health threshold behavior:** Below 40% health, the Prince becomes aggressive — abandons protective positioning and attacks directly. The Princess does not react to this change with grief or hesitation. She uses the opening he creates.
**Drop:** One Draught of Vitality, one Sorcerer's Salve
**Notes:** Fighting the Prince and Princess requires the player to recognize the dynamic and consciously target the Princess despite the Prince's interposition. The Comet Staff's splash can damage both simultaneously. The Obliterator Stave's tendrils hit both regardless of positioning.

---

#### Demonic Princess
**Health:** 120%
**Movement:** Standard — she moves to maintain optimal casting range, not to close with the player
**Attacks:**
- Arcane bolt volley — 15% per bolt, 3 bolts per cast, rapid succession
- Sustained beam — 8% per second, 4 second duration, significant warning (visual charge-up)
- Disorientation pulse — no damage, applies disorientation effect (screen distortion, inverted controls for 3 seconds)
**Behavior:** She casts. She uses the Prince as her shield. She will sacrifice him if it creates an opening. Once the Prince falls she becomes more mobile, maintaining distance rather than static positioning. The disorientation pulse is used reactively — when the player closes to melee range.
**Drop:** One Draught of Vitality, one Comet Core
**Notes:** The Circlet of Warding halves the disorientation duration. Without it, the 3-second control inversion is severely punishing in a room with an active elite caster. This encounter is the primary motivation for acquiring the Circlet before entering Ashenmoor.

---

#### Demonic Knight
**Health:** 90%
**Movement:** Standard — deliberate, never hurried
**Attack:** Greatsword — 30% damage, melee, slow wind-up with a brief tell
**Behavior:** The seven knights in the dungeon corridor do not patrol — they stand at intervals along the walls. They activate when the player crosses a threshold midway down the corridor, all seven simultaneously. They advance in formation, spacing maintained, filling the corridor width. They cannot be kited backward past the threshold — it is a one-way trigger.
**Drop:** Storm Flux, Arcane Plasma Vials
**Notes:** This is the hardest combat encounter in the game before the finale. The corridor is narrow — the Comet Staff's self-damage risk is significant. The Obliterator Stave is the intended tool if the player has conserved it. The Tempest Rod's sustained fire handles knights individually but seven simultaneous activations require area solutions.

---

#### The Necromancer
**Health:** 200%
**Role:** The Banished Lord's servant and the portal's co-architect. Is destroyed in the resurrection sequence by the player's autonomous spell-casting.

---

#### The Master
**Health:** 250%
**Role:** The player's master, revealed as the Banished Lord's ally and the portal's co-architect. Does not engage in combat. Is destroyed in the resurrection sequence by the player's autonomous spell-casting.
**Notes:** The Master's betrayal is the narrative's primary reversal. His death in the resurrection sequence — destroyed by his own apprentice, involuntarily, through a power the apprentice didn't know they had — is the story's thematic resolution. His character detail is in `narrative.md`.

---

#### Banished Lord
**Health:** 300%
**Role:** Scripted finale only. The Lord does not engage in standard combat. He stands, observes, and executes the scripted beheading when the player attempts to interrupt the portal formation.
**The beheading:** Scripted trigger — when the player fires any weapon at the Master or the portal, the Lord moves. One action. Instantaneous. The player cannot dodge it, block it, or prevent it. It is not a failure state.
**Notes:** The Lord's design communicates that he is not something the player fights — he is something the player survives. His role in the finale is to demonstrate that the player's conventional agency has run out, which is what makes the resurrection sequence's unconventional agency meaningful.

---

## 7. NPC and Dialogue System

### Overview

NPC dialogue is implemented as branching conversation trees triggered by proximity and player input. Conversations pause gameplay. Quest flags control which dialogue options are available — NPCs respond to what the player has done.

### Conversation Structure

Each NPC has:
- **Greeting line** — varies based on quest flag state. Father Cassian greets a stranger differently than he greets someone who has spoken to Maret about the wizard.
- **Topic menu** — a list of selectable topics. Topics appear and disappear based on quest flags.
- **Exit line** — brief, consistent with character. Not a dismissal.

### Quest Flag Integration

Dialogue branches check flags before displaying. Example:

```
IF RELIC_ACQUIRED = false AND ORVYN_SPOKEN = true
    Father Cassian → Topic: "The Relic" → AVAILABLE
ELSE IF RELIC_ACQUIRED = true
    Father Cassian → Topic: "The Relic" → REPLACED WITH "Safe travels"
```

Full flag list in Section 8.

### Shop Integration

Vendor NPCs (Aldra, Brother Oswin, Maret, Tomlin) have a "Trade" topic that opens the shop interface. The shop interface is a separate screen — not embedded in the conversation tree.

### One-Time Dialogue

Certain lines play only once — primarily lore and atmosphere lines that would feel repetitive on repeat visits. These are flagged internally and replaced with shorter acknowledgment lines on subsequent visits.

---

## 8. Quest Flag System

All quest progression is tracked through boolean flags. No quest journal is displayed to the player.

### Flag List

| Flag | Set When | Used For |
|---|---|---|
| `TUTORIAL_COMPLETE` | Couple escorted to Thornwall gate | Unlocks town NPC full dialogue |
| `THORNWALL_ENTERED` | Player passes through main gate | Thornwall ambient state change |
| `ORVYN_SPOKEN` | King Orvyn's full briefing completed | Unlocks Relic topic with Father Cassian |
| `RELIC_ACQUIRED` | Relic picked up from vestry | Removes Relic topic from Cassian, adds it to Maret |
| `MARET_WARNED` | Maret's dark pool dialogue completed | Optional — adds dialogue option at the pool |
| `HUNGERING_BRANCH_UNLOCKED` | Full Maret conversation completed | Adds Hungering Branch to her inventory |
| `COUPLE_FOUND` | Player speaks to Sela and Davan in town | Triggers Bread and Salt gift |
| `WYCHFELD_ENTERED` | Player leaves Thornwall north gate | Locks return to Thornwall (one-way) |
| `GEST_MET` | Player speaks to Gest | Unlocks wolf patrol pattern dialogue |
| `GEST_ERRAND_COMPLETE` | Optional errand completed | Gest provides additional intelligence |
| `WRAITH_SUMMONED` | Relic used at dark pool | Required for moat entry |
| `MOAT_ENTERED` | Player enters moat | One-way — Wychfeld locked permanently |
| `BARBICAN_CLEAR` | Both barbican sentries dead | Triggers first autosave in Ashenmoor |
| `COURTYARD_CLEAR` | All courtyard enemies dead | Unlocks great hall door |
| `FEAST_CLEAR` | All hall enemies dead | Unlocks chambers access |
| `PRINCE_DEAD` | Prince defeated | Partial chambers clear |
| `PRINCESS_DEAD` | Princess defeated | Full chambers clear, triggers second autosave |
| `HATCHWAY_FOUND` | Player discovers and uses hatchway | Required for dungeon access — cannot be skipped |
| `KNIGHTS_DEAD` | All seven corridor knights dead | Unlocks deepest cell door |
| `FINALE_TRIGGERED` | Player fires weapon in deepest cell | Initiates scripted finale sequence |

---

## 9. Shop System

### Currency

A single currency type — name and visual to be determined by art direction. Earned by selling found items (not implemented in initial scope — simplify to fixed found amounts) or found as pickups in the environment. Thornwall is the only location with vendors.

### Vendor Inventories

#### Aldra (Blacksmith)
| Item | Price |
|---|---|
| Warded Travel Cloak | 3 currency |
| Scatterstaff | 2 currency |
| Bone Pellet Mana ×10 | 1 currency |

#### Brother Oswin (Apothecary)
| Item | Price |
|---|---|
| Tincture of Mending | 1 currency |
| Mana Vial | 1 currency |

#### Maret (Hedge-Witch)
| Item | Price | Condition |
|---|---|---|
| Ghostlight Torch | 2 currency | Always available |
| Sorcerer's Salve | 3 currency | Always available |
| Hungering Branch | 0 currency (gift) | `HUNGERING_BRANCH_UNLOCKED` = true |

### Shop Interface

A simple grid display — item icon, item name, effect description, price. Player confirms purchase. Currency deducted. Item added to inventory. No haggling, no restock timer — vendors have unlimited stock of listed items.

---

## 10. Inventory and UI

### Inventory Screen

Accessed via dedicated key. Pauses gameplay. Three panels:

**Weapons panel** — lists all acquired weapons with current ammunition count. Active weapon highlighted. Player selects to switch active weapon.

**Equipment panel** — four armor slots displayed. Current equipped item shown in each slot. Player selects a slot to cycle through acquired items for that slot.

**Consumables panel** — lists all carried consumables with stack counts. Player sets the active consumable slot from here.

### HUD

Minimal. Four elements displayed during gameplay:

| Element | Position | Display |
|---|---|---|
| Health | Lower left | Flame or candle indicator — full flame = full health, guttering = low |
| Active weapon mana | Lower right | Fill bar — depletes as ammo is used |
| Active consumable | Lower right (above mana) | Item icon and stack count |
| Air supply (moat only) | Upper center | Bubble indicator — appears only during moat sequence |

No numerical readouts. No minimap. No crosshair by default — UZDoom's autoaim handles close and mid-range targeting. Optional crosshair toggle in settings for accessibility.

---

## 11. Save System

### Autosave Points

Three autosave checkpoints. Saving is automatic — no player input required. No manual save option.

| Checkpoint | Trigger Flag | Location |
|---|---|---|
| Thornwall Hub | `THORNWALL_ENTERED` (and any re-entry) | Thornwall — any return to hub |
| Ashenmoor Courtyard | `BARBICAN_CLEAR` | Post-barbican, pre-courtyard |
| Ashenmoor Chambers | `PRINCESS_DEAD` | Post-chambers boss encounter |

### Save State

Each save records:
- Current health
- All weapon states and ammunition counts
- All armor equipped
- All consumable inventory
- All quest flags
- Player position at checkpoint location (not mid-level position)

On death, the player reloads at the checkpoint location with the saved state. They do not return to their exact death position.

### Thornwall Re-entry

If the player returns to Thornwall after acquiring the Relic but before using it (possible — `WYCHFELD_ENTERED` is not set until the north gate is passed), the game autosaves. NPC dialogue updates to reflect the player's readiness to depart.

---

## 12. Moat Swim Sequence

### Overview

The moat sequence is the game's most mechanically unique moment and carries its own dedicated section due to the implementation risk identified in `tech_overview.md`. It must be prototyped in Phase 1.

### Sequence Description

The player is drawn into the moat by the Water-Wraith. The camera orientation on entry is randomized within a defined range — the player does not know which direction the surface is. The surface is not up — the underground channel feeding the moat means the surface access point is to the north, not above.

### Mechanics

**Air supply:** 30 seconds from submersion. Displayed as a bubble indicator on the HUD — appears only during this sequence. At 0 seconds, health begins depleting at 5% per second.

**Disorientation:** On entry, the camera pitches and rolls briefly (2 seconds) before settling into a disoriented-but-stable first-person view. The Circlet of Warding reduces this to 1 second. The player retains full control during disorientation — they just don't know which way they're pointing.

**Navigation:** The correct direction (north, toward the embankment) is indicated by a faint bioluminescent glow — the same cold green of the dungeon below, surfacing through the moat floor in that direction only. It is subtle. Players who miss it will find it by process of elimination within the air timer.

**Combat:** No enemies in the moat. This is a traversal and atmosphere sequence, not a combat encounter. The shapes visible in the water are non-interactive.

**Exit:** The embankment is a climbable ledge on the northern bank. The player pulls themselves out and the moat sequence ends. Normal gameplay resumes. The third-person perspective pull-out animation (if implemented) is brief.

### UZDoom Implementation Notes

Standard UZDoom does not natively support a disoriented swim sequence with non-standard gravity orientation. The following approaches should be evaluated in Phase 1 prototyping:

- **Sector-based water with scripted camera pitch** — use UZDoom's water sector type with ZScript camera manipulation during the entry sequence
- **Gravity inversion sector** — use a custom gravity direction for the moat sector that redirects "up" to north, making swimming feel natural once the player orients
- **Scripted pull sequence** — treat the wraith's drawing-in as a brief scripted movement that deposits the player in the moat already moving in the correct general direction, reducing the disorientation mechanic to atmospheric camera shake rather than genuine directional confusion

The third option is the fallback if the first two prove impractical within UZDoom's constraints. The narrative beat — the wraith's passage, the water, the disorientation, the surface — is more important than the specific implementation of directional ambiguity. A compelling swim sequence that works is better than a technically ambitious one that doesn't.

---

*All values in this document are first-pass estimates subject to revision during playtesting. Flag any balance issues in the decision log with the phase number and playtester feedback.*