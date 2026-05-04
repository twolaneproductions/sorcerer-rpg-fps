# levels.md
## Ashenmoor — Level Design
**OUR NEW INDIE GAME STUDIO**
**Version:** 0.1
**Last Updated:** 2026-04-26
**Status:** Phase 0 — Draft

---

- [levels.md](#levelsmd)
  - [Ashenmoor — Level Design](#ashenmoor--level-design)
  - [Document Conventions](#document-conventions)
  - [Level 00 — Tutorial Woods](#level-00--tutorial-woods)
    - [Overview](#overview)
    - [Layout](#layout)
    - [Enemies](#enemies)
    - [Items](#items)
    - [NPCs](#npcs)
    - [Quest Flags](#quest-flags)
    - [Entry / Exit](#entry--exit)
    - [Atmosphere Notes](#atmosphere-notes)
  - [Level 01 — Thornwall](#level-01--thornwall)
    - [Overview](#overview-1)
    - [Layout](#layout-1)
    - [Enemies](#enemies-1)
    - [Items](#items-1)
    - [NPCs](#npcs-1)
    - [Quest Flags](#quest-flags-1)
    - [Entry / Exit](#entry--exit-1)
    - [Atmosphere Notes](#atmosphere-notes-1)
  - [Level 02 — Thornwall Castle](#level-02--thornwall-castle)
    - [Overview](#overview-2)
    - [Layout](#layout-2)
    - [Enemies](#enemies-2)
    - [Items](#items-2)
    - [NPCs](#npcs-2)
    - [Quest Flags](#quest-flags-2)
    - [Entry / Exit](#entry--exit-2)
    - [Atmosphere Notes](#atmosphere-notes-2)
  - [Level 03 — The Wychfeld](#level-03--the-wychfeld)
    - [Overview](#overview-3)
    - [Sub-zone 03A — Amber Fields](#sub-zone-03a--amber-fields)
    - [Sub-zone 03B — Greywood](#sub-zone-03b--greywood)
    - [Sub-zone 03C — Ashenmoor Approach](#sub-zone-03c--ashenmoor-approach)
    - [Outer Ruins and Dark Pool](#outer-ruins-and-dark-pool)
  - [Level 04 — The Moat](#level-04--the-moat)
    - [Overview](#overview-4)
    - [Layout](#layout-3)
    - [Enemies](#enemies-3)
    - [Items](#items-3)
    - [Quest Flags](#quest-flags-3)
    - [Entry / Exit](#entry--exit-3)
    - [Atmosphere Notes](#atmosphere-notes-3)
  - [Level 05 — Ashenmoor: Barbican and Courtyard](#level-05--ashenmoor-barbican-and-courtyard)
    - [Overview](#overview-5)
    - [Layout](#layout-4)
    - [Enemies](#enemies-4)
    - [Items](#items-4)
    - [Quest Flags](#quest-flags-4)
    - [Entry / Exit](#entry--exit-4)
    - [Atmosphere Notes](#atmosphere-notes-4)
  - [Level 06 — Ashenmoor: Great Hall](#level-06--ashenmoor-great-hall)
    - [Overview](#overview-6)
    - [Layout](#layout-5)
    - [Enemies](#enemies-5)
    - [Items](#items-5)
    - [Quest Flags](#quest-flags-5)
    - [Entry / Exit](#entry--exit-5)
    - [Atmosphere Notes](#atmosphere-notes-5)
  - [Level 07 — Ashenmoor: Chambers](#level-07--ashenmoor-chambers)
    - [Overview](#overview-7)
    - [Layout](#layout-6)
    - [Enemies](#enemies-6)
    - [Items](#items-6)
    - [Quest Flags](#quest-flags-6)
    - [Entry / Exit](#entry--exit-6)
    - [Atmosphere Notes](#atmosphere-notes-6)
  - [Level 08 — Ashenmoor: Dungeons](#level-08--ashenmoor-dungeons)
    - [Overview](#overview-8)
    - [Layout](#layout-7)
    - [Enemies](#enemies-7)
    - [Items](#items-7)
    - [Quest Flags](#quest-flags-7)
    - [Entry / Exit](#entry--exit-7)
    - [Atmosphere Notes](#atmosphere-notes-7)
  - [Level 09 — Ashenmoor: The Deepest Cell (Finale)](#level-09--ashenmoor-the-deepest-cell-finale)
    - [Overview](#overview-9)
    - [Layout](#layout-8)
    - [Scripted Sequence (post-beheading)](#scripted-sequence-post-beheading)
    - [Items](#items-8)
    - [Quest Flags](#quest-flags-8)
    - [Entry / Exit](#entry--exit-8)
    - [Atmosphere Notes](#atmosphere-notes-8)


## Document Conventions

Each level entry follows the same template:
- **Overview** — narrative and mechanical purpose of the zone
- **Layout** — spatial description, room by room or area by area
- **Enemies** — what spawns, where, in what configuration
- **Items** — every pickup and its location
- **NPCs** — who is present and where
- **Quest flags** — what is checked and what is set
- **Entry / Exit** — how the player arrives and how they leave
- **Atmosphere notes** — lighting, sound, environmental detail for implementation

All item and enemy counts are first-pass estimates subject to playtesting revision.

---

## Level 00 — Tutorial Woods

### Overview
The game's opening zone. Introduces movement, the Witch Switch, and basic combat before the player reaches Thornwall. Establishes the threat in the woods and gives the player their first connection to Thornwall — the couple in trouble. Short, linear, low difficulty.

### Layout
A narrow forest path leading from an implied point of origin in the south toward Thornwall's gate, visible at the path's northern end. The path curves twice to obscure the full length — the player should not see the gate until they have cleared the encounter.

**Area A — The Approach:** The player begins walking north. Ambient sound only — wind, distant owl, creaking branches. No enemies. 20–30 seconds of walking to establish tone.

**Area B — The Encounter:** The path widens into a small clearing. Sela and Davan are cornered against a fallen tree by three demonic wolves. The wolves are engaged with the couple and do not immediately notice the player — a moment to assess before combat triggers.

**Area C — The Escort:** Once the wolves are dead, brief dialogue, then the escort to the gate — 60–90 seconds of walking. Two additional wolves spawn partway through from the tree line. The couple huddles close and does not fight.

### Enemies
- Area B: 3 demonic wolves (pre-positioned, engaged with couple)
- Area C: 2 demonic wolves (mid-escort spawn from tree line)

### Items
- Area A: 1 Tincture of Mending — beside the path, visible but not obvious. Teaches the player to look.
- Area B: 1 Bone Pellet Mana — dropped by wolves. Introduces the ammo type before the Scatterstaff is available.

### NPCs
- Sela and Davan — Area B, post-combat. Brief dialogue. Sela speaks. Davan is quiet.

### Quest Flags
- `TUTORIAL_COMPLETE` — set when the couple reaches the gate -- without it, entry isn't granted

### Entry / Exit
- Entry: Game start
- Exit: Thornwall main gate — automatic transition on reaching the gate with the couple

### Atmosphere Notes
- Night or deep dusk. Torch light visible from the gate ahead.
- Wolf silence is the key audio note — no howling, only the sound of movement when close.
- The gate guards react to the player's arrival with the couple — brief exchange at the threshold.

---

## Level 01 — Thornwall

### Overview
The game's hub. All vendors, all primary NPCs, and all pre-departure quest activity. The player can enter after `TUTORIAL_COMPLETE` is set and may return until `WYCHFELD_ENTERED` is set, after which Thornwall is inaccessible.

Not a combat zone. The threat is atmospheric — in what NPCs say, in the shrine by the gate, in the barricaded windows of some buildings.

### Layout
A compact town — six key buildings arranged around a central cobblestone lane, with the church at the northern end and the castle road branching off the midpoint.

**The Gate Area:** Main gate, guard post, shrine. The two escort guards are stationed here. The shrine is immediately visible on entry.

**The Main Lane:** Central spine of town.
- The Broken Antler tavern (Hobb) on the left midway.
- The Green Mortar apothecary (Brother Oswin) on the right.
- The Hammer Song smithy (Aldra) at the southern end — heard before seen.

**The Side Alley:** A narrow turning off the main lane leads to the Crooked Candle (Maret). Slightly set apart, slightly harder to find.

**The Church:** Northern end of the lane, before the castle road branches. Father Cassian inside.

**The Residential Quarter:** East of the main lane. Sela and Davan's home. The player finds them here if they seek them out.

**The Castle Road:** Branches north from the church area. Short cobblestone approach to Thornwall Castle's outer gate.

### Enemies
None.

### Items
Available for purchase — see [GDD_systems.md Section 9](./GDD_systems.md#9-shop-system). No free pickups in Thornwall.

**Exceptions:** Harwen (Thornwall Castle) gives 2 Tincts of Mending. Sela and Davan give Bread and Salt if found.

### NPCs
- Guard (young, red-haired) — gate, outside
- Hobb — Broken Antler, inside
- Brother Oswin — Green Mortar, inside
- Aldra — Hammer and Song, forge area
- Maret — Crooked Candle, inside
- Father Cassian — Church of the Pale Candle, vestry area
- Sela and Davan — residential quarter

### Quest Flags
- `THORNWALL_ENTERED` — set on entry (autosave)
- `RELIC_ACQUIRED` — set when Relic taken from Father Cassian's vestry
- `COUPLE_FOUND` — set when player speaks to Sela and Davan
- `HUNGERING_BRANCH_UNLOCKED` — set after Maret's full conversation

### Entry / Exit
- Entry: From tutorial woods (first visit) or Wychfeld south road (return visits)
- Exit: Castle road → Level 02, or north gate → Wychfeld (sets `WYCHFELD_ENTERED`, one-way)

### Atmosphere Notes
- Daytime — warm, amber. Fires visible through windows at dusk if player lingers.
- The shrine grows slightly between visits if the player returns.
- Aldra's hammer audible from the main lane. The most comforting sound in the game.
- Dogs stay close to doorways. No children visible outdoors.

---

## Level 02 — Thornwall Castle

### Overview
A single-visit zone. The player gains access after a small magic demonstration, receives the quest from King Orvyn, collects Harwen's gift, and departs. Not a combat zone. Sets the narrative stakes.

### Layout
**The Outer Gate:** Two guards. The junior guard requires the magic demonstration — one Witch Switch bolt is sufficient.

**The Outer Bailey:** Training ground east, stable west. Captain Amis observing the drilling soldiers.

**The Great Hall:** Map table, advisors, Steward Aldric. Aldric intercepts the player before the throne room.

**The Throne Room:** King Orvyn. The quest briefing. The wizard's portrait on the wall — clearly an old friend. The covered portrait at the far end — present, briefly visible, no one will discuss it.

**The Side Corridor:** Harwen's room — small, book-filled. He gives the Tincts and speaks of the wizard.

**The Page:** Emmet runs messages between the hall and throne room. The player can intercept him.

### Enemies
None.

### Items
- 2 Tincts of Mending — given by Harwen, not found as pickups

### NPCs
- Gate guards (senior and junior) — outer gate
- Captain Amis — outer bailey
- Steward Aldric — great hall
- King Orvyn — throne room
- Harwen — side corridor
- Emmet — great hall and corridor, moving

### Quest Flags
- `ORVYN_SPOKEN` — set on completing King Orvyn's full briefing

### Entry / Exit
- Entry: From Thornwall castle road
- Exit: Return to Thornwall — the only exit

### Atmosphere Notes
- Interior stone, high ceilings, plenty of windows, lit candles everywhere at night.
- Emmet is always in motion. Catching him for dialogue feels like intercepting a busy person.
- The covered portrait is at the far end of the throne room. Not interactive. Observed at distance only.

---

## Level 03 — The Wychfeld

### Overview
The overworld traversal — three sub-zones in sequence with one optional branch. Primary combat zone before the castle. Designed to take approximately 15–18 minutes. Establishes the dread of what lies ahead through escalating environmental wrongness and enemy presence.

---

### Sub-zone 03A — Amber Fields

**Overview:** Former farmland, now abandoned and grey. Open terrain, long sightlines. First Wychfeld combat. One optional NPC (Gest).

**Layout:**
The King's Road runs straight north through the fields. Farmhouses at intervals — doors open, contents visible.

**Gest's Farmhouse:** Third farmhouse on the right, slightly larger. Gest is barricaded inside, visible through a window. Interact with the door to be admitted. Her optional errand — retrieving an item from the farmhouse two buildings north — requires one wolf encounter. Reward: wolf patrol intelligence (dialogue), one Sorcerer's Salve.

**Enemies:**
- 4 demonic wolves — loose patrol across the fields in two pairs
- 2 additional wolves near Gest's errand farmhouse

**Items:**
- 1 Tincture of Mending — inside first farmhouse on left, on a table
- 1 Mana Vial — beside the road, near the chiseled milestone
- 1 Bone Pellet Mana ×5 — wolf drops
- 1 Sorcerer's Salve — Gest's errand reward

**Quest Flags:**
- `GEST_MET` — set on speaking to Gest
- `GEST_ERRAND_COMPLETE` — set on completing errand and returning

---

### Sub-zone 03B — Greywood

**Overview:** Forest, darker and more oppressive than the fields. Goblins replace wolves. The Woodcutter's Chapel is the zone's rest point.

**Layout:**
The King's Road continues north, enclosed by close-pressing trees.

**Goblin Camp — West of Road:** Visible from the road. Three patrol goblins, one commander inside. Optional — avoidable by staying on the road. Contains the Scatterstaff if not purchased in Thornwall.

**Goblin Camp — Blocking the Road:** Partially blocks the road with a crude barricade. Unavoidable. Four goblins, one commander.

**The Woodcutter's Chapel:** Set back from the road at a crossroads within the forest. Candles burning inside without apparent source. No enemies will enter or spawn near it. Safe point for consumable use — no autosave.

**Enemies:**
- Optional western camp: 3 goblins, 1 commander
- Road-blocking camp: 4 goblins, 1 commander

**Items:**
- 1 Mana Vial — inside the Woodcutter's Chapel
- 1 Tincture of Mending — inside the Woodcutter's Chapel
- 1 Scatterstaff — optional western camp, commander drop (if not purchased in Thornwall)
- Storm Flux ×20 — goblin drops across both camps
- 1 Ghostlight Torch — optional western camp, chest

**Quest Flags:** None specific. Road barricade camp is the only mandatory combat.

---

### Sub-zone 03C — Ashenmoor Approach

**Overview:** The forest thins. The land opens into blighted former farmland. No enemies. Environmental storytelling only. The castle becomes fully visible. The **WALLS** that bar off entry even to the moat are seen.

**Layout:**
The road emerges from the Greywood into cracked black earth in geometric patterns. Farmhouses in worse condition than the Amber Fields — violent departure rather than orderly evacuation. Then the road ends before the moat at heavy, dark clouds that form an impenetrable wall around the castle.

Ashenmoor's outer ruins are visible ahead. The dark pool is visible to the north — perfectly still, catching no light. Hundreds of crows line the dead fields, facing north, silent.

Approximately 90 seconds of walking with no combat. Deliberate pacing — a decompression beat before the castle's density begins.

**Items:** None. The approach is empty by design.

**Quest Flags:**
- `ASHENMOOR_APPROACHED` — set on reaching the impenetrable wall

---

### Outer Ruins and Dark Pool

**Overview:** Point of no return. The conventional approach to the castle is blocked. The wraith is summoned at the dark pool.

**Layout:**
The outer ruins are a collapsed curtain wall. The conventional path is blocked — rubble, wardings, wrong. One corrupted soldier in the gatehouse (avoidable).

The dark pool is a hollow north of the ruins. Still, iridescent, bottomless-looking. Scratch marks on the stones at the waterline.

**The Summoning:** Player uses the Relic from inventory near the pool. It shatters on the water's surface. The wraith rises. Brief dialogue — recognition, the pressing of the amulet into the player's hand, the drawing down.

**Enemies:**
- 1 corrupted soldier — outer gatehouse (optional, avoidable)

**Items:**
- The Wizard's Own Amulet — auto-added to inventory during summoning
- Shard of the Relic — replaces the Relic in inventory after summoning

**Quest Flags:**
- `WRAITH_SUMMONED` — set on using the Relic at the pool
- `MOAT_ENTERED` — set when the player is pulled under (permanent, one-way)

**Entry / Exit:**
- Entry: From Ashenmoor Approach
- Exit: Into the moat — one-way

---

## Level 04 — The Moat

### Overview
A traversal and atmosphere sequence. No combat. The player is submerged, disoriented, and must find the embankment exit before the air timer expires. Full mechanical specification in [GDD_systems.md Section 12](./GDD_systems.md#12-moat-swim-sequence).

### Layout
The moat is dark water surrounding the castle perimeter. The player enters from the southern channel. The embankment exit is on the northern bank — swimming north and slightly up.

The correct direction is indicated by a faint bioluminescent glow from the moat floor to the north. Subtle but findable within the air timer.

Shapes drift in the water — non-interactive, non-aggressive. Humanoid in suggestion only.

### Enemies
None.

### Items
None.

### Quest Flags
- `MOAT_ENTERED` — already set on entry

### Entry / Exit
- Entry: From dark pool summoning (scripted)
- Exit: eastern embankment — player climbs out, normal gameplay resumes

### Atmosphere Notes
- The bioluminescent glow is the only light source. Everything else is near-black.
- Muffled ambient sound only.
- The air bubble HUD element appears only during this sequence.

---

## Level 05 — Ashenmoor: Barbican and Courtyard

### Overview
First combat inside the castle perimeter. The player emerges from the moat into real threat. Two distinct areas — the narrow barbican passage and the open courtyard. First Ashenmoor autosave at courtyard entry.

### Layout
**The Embankment:** Narrow stone ledge between the moat and the drawbridge. The drawbridge is down.

**The Barbican:** A vaulted passage through the gatehouse, approximately 20 meters long. Two corrupted soldiers — one at each end. The defaced protective inscriptions are visible on the walls.

**The Courtyard:** Wide, irregular, fire pits burning. Demonic peasants milling around the fires. The sealed well at the center — warm iron plate, bolted from outside. The stable block along the eastern wall — silent horses facing the wall. Great hall door at the northern end.

**Autosave trigger:** `BARBICAN_CLEAR` — both barbican soldiers dead.

### Enemies
- Barbican: 2 corrupted soldiers
- Courtyard: 6 demonic peasants, 1 additional soldier near the great hall door

### Items
- 1 Tincture of Mending — near the first fire pit
- 1 Mana Vial — inside the stable block
- Arcane Plasma Vials ×15 — dropped by courtyard soldier
- The Comet Staff — propped against the sealed well housing. Unmissable.

### Quest Flags
- `BARBICAN_CLEAR` — set when both barbican soldiers dead (triggers autosave)
- `COURTYARD_CLEAR` — set when all courtyard enemies dead (unlocks great hall door)

### Entry / Exit
- Entry: From eastern embankment (post-moat)
- Exit: Great hall door, western end of courtyard

### Atmosphere Notes
- Courtyard fires burn orange-red.
- The demonic peasants hum lowly, zombie-like.
- The sealed well hisses and steams, like the water is boiling.
- The stable horses are an optional visual. No enemy spawns inside the stable.

---

## Level 06 — Ashenmoor: Great Hall

### Overview
The feast encounter. A mid-sized combat space with a minstrel playing in the corner. The Magestream Wand is found here. The Latin choir becomes barely audible for the first time.

### Layout
**The Hall:** Long trestle tables, food in various states of decay, iron chandeliers with burning candles. Modified tapestries on the walls — the silver hawk on black with dark additions.

**The Minstrel's Corner:** Southwest corner. A figure on a stool with an out-of-tune instrument. He plays continuously throughout the encounter. He does not fight. He does not react to combat. Killing him is optional and has no mechanical consequence. His death silences the music.

**The Far Door:** Hall's northern end, short corridor to the chambers. Locked until `FEAST_CLEAR` is set. Iron-banded oak, carved with a kneeling figure motif.

### Enemies
- 8 demonic peasants — seated at or standing near the tables
- 2 corrupted soldiers — stationed at the far door, backs to the player on entry
- The minstrel — non-hostile, killable

### Items
- The Magestream Wand — behind the feast table on a serving ledge. Visible from the entrance.
- 1 Draught of Vitality — inside a stuck cabinet off the main hall (interact to open, no key needed)
- Arcane Plasma Vials ×20 — on the serving table near the Magestream Wand
- 1 Mana Vial — dropped by soldiers

### Quest Flags
- `FEAST_CLEAR` — set when all hostile enemies dead (unlocks far door for new enemy entry)

### Entry / Exit
- Entry: From courtyard great hall door
- Exit: Far door corridor → chambers

### Atmosphere Notes
- The Latin choir: barely audible here. A single voice.
- The feast food is real and recently cooked.
- The minstrel's instrument is out of tune.

---

## Level 07 — Ashenmoor: Chambers

### Overview
The private quarters. The Demonic Prince and Princess encounter — the primary boss fight. Second autosave triggers after their defeat. The hatchway to the dungeons is found here.

### Layout
**The Antechamber:** Short corridor off the great hall. Overturned furniture, mirrors covered with black cloth, windows sealed with pulled tapestry. Two minor enemies.

**The Main Chamber:** Larger space. The Prince toward the center, the Princess near the far wall. The room's furniture has been rearranged by the Princess — pushed to the walls in a pattern forming a partial geometric figure that echoes the ritual figure in the deepest cell.

**The Hatchway:** After the encounter, behind a displaced wardrobe on the eastern wall. Iron ring in the floor, recently oiled hinges, stairs descending. Required to find — the player cannot proceed without it. Not hidden but requires looking.

**Autosave trigger:** `PRINCE_DEAD` and `PRINCESS_DEAD` — second Ashenmoor autosave.

### Enemies
- Antechamber: 1 skeleton, 1 zombie
- Main Chamber: The Demonic Prince and Princess (full specifications in [GDD_systems.md Section 6](./GDD_systems.md#6-enemy-roster))

### Items
- 1 Draught of Vitality and 1 Sorcerer's Salve — dropped by the Prince
- 1 Draught of Vitality and 1 Comet Core — dropped by the Princess
- Soul Confluence ×1 — on a stand near the far wall, lootable post-combat
- 1 Tincture of Mending — antechamber surface

### Quest Flags
- `PRINCE_DEAD` — set on Prince's death
- `PRINCESS_DEAD` — set on Princess's death (triggers autosave)
- `HATCHWAY_FOUND` — set when player descends the hatchway stairs

### Entry / Exit
- Entry: From great hall corridor
- Exit: Hatchway stairs → upper dungeon

### Atmosphere Notes
- The covered mirrors can be uncovered by the player — a face that is not quite the player's looks back. Purely atmospheric.
- Latin choir: two or three voices, clearer.

---

## Level 08 — Ashenmoor: Dungeons

### Overview
Two sections — the upper dungeon and the dungeon corridor approach. The Latin choir grows throughout. Light transitions from orange torchlight to bioluminescent green to cold silver. The hardest sustained combat before the finale.

### Layout
**The Upper Dungeon:** Stone corridors, iron-bar cells on both sides. Orange torchlit in the upper section. Several cells contain things that were here before the castle fell. The cells are locked.

**The Light Transition:** Through the descent, orange torchlight give way to green bioluminescent glow sourced from below.

**The Dungeon Corridor:** A long vaulted passage. Cold silver fires in iron sconces — distinct from both orange above and green below. Seven Demonic Knights standing at intervals along the walls, motionless, visors down.

The activation threshold is a visible floor seam — a change in stonework approximately halfway down the corridor. Crossing it activates the first of the seven Knights.

The corridor is narrow — two people abreast at most. The Obliterator Stave clears it efficiently. Two Soul Confluence charges are placed immediately before the threshold — the player finds the Stave's rarest ammunition directly before the encounter that needs it most.

**The Deepest Cell Door:** At the corridor's far end. Not locked. Opens inward. Silently.

### Enemies
- Upper Dungeon: 4 skeletons in two patrolling pairs, 2 stationary zombies near the light transition
- Dungeon Corridor: 7 Demonic Knights encountered one after the next.

### Items
- 1 Tincture of Mending — upper dungeon guard table
- Storm Flux ×30 — skeleton drops
- Arcane Plasma Vials ×20 — zombie drops
- Soul Confluence ×2 — in two sconce alcoves in the corridor, before the threshold
- Various ammo — knight drops

### Quest Flags
- `KNIGHTS_DEAD` — set when all seven corridor knights are dead (deepest cell door opens)

### Entry / Exit
- Entry: Hatchway stairs from chambers
- Exit: Deepest cell door → Level 09

### Atmosphere Notes
- Latin choir: full and complex in the upper dungeon — legitimate prayer. In the corridor, the words begin to shift. Syllables that don't belong. Rhythm becoming wrong.
- Three distinct light sources across three distinct zones: orange above, green mid-descent, cold silver in the corridor.
- The player's own breathing becomes audible in the corridor during the silence before threshold crossing.

---

## Level 09 — Ashenmoor: The Deepest Cell (Finale)

### Overview
The game's final sequence. Three Boss figures to combat at once: The Master, the Warlock (both of whom alternatively try to keep the portal open), and the Banished Lord. Entirely scripted after `FINALE_TRIGGERED` is set. The beheading. The resurrection. The destruction.

### Layout
**The Cell:** Largest room in the castle. A vast geometric figure inscribed on the floor. Candles at the figure's vertices burning with pale silver light. The portal at the far end — a seam in the air, cycling through unnatural colors (neon pink, electric blue, and vivid green -- the first such instance of these colors).

The Master stands with his back to the door, arms raised, reciting. The Demonic Warlock kneels at the figure's center. The Banished Lord sits at the Warlock's shoulder, leaning on his sword, facing the door, absolutely still.

The player must kill the Master and Demonic Warlock and sufficiently wound the Banished Lord to set `FINALE_TRIGGERED`.

**FINALE_TRIGGERED:** The Banished Lord suddenly rises and beheads the player then resurrects the Master and Warlock to reopen the portal.

### Scripted Sequence (post-beheading)

1. Player perspective drops to floor level — the severed head's view
2. The room continues. The Master recites. The portal grows.
3. Several seconds of silence and stillness.
4. A single syllable — barely voiced — the first incantation from the severed head.
5. The body twitches. Blood pools, then begins to bubble.
6. Magical sparks from the neck stump, increasing in intensity.
7. The body rises. *Brief constrained control returns to the player.*
8. Spellcasting begins — the player's input casts new spells simply from his bare hands.
9.  The portal — something huge is crawling out, but when the Apprentice casts his spell, the portal collapses inward.
10. The foundations — collapse begins from the deepest cell outward, rising through dungeon, chambers, hall, courtyard, burrying the four magic users underneath it all.
11. Player perspective rises with the collapsing castle — carried up through the zones in fast vertical motion as rubble falls.
12. White. Then silence.

### Items
None.

### Quest Flags
- `FINALE_TRIGGERED` — set upon defeating the Banished Lord, Warlock, and Master.

### Entry / Exit
- Entry: Dungeon corridor, deepest cell door
- Exit: Game end — credits or title screen return

### Atmosphere Notes
- Latin choir at maximum distortion on entry.
- The choir cuts to near-silence the moment the player crosses the cell threshold.
- The beheading is the loudest single sound in the game. The subsequent silence is the longest.
- The resurrection's visual escalation — blood to sparks to spell fire to collapse — is the most visually intense sequence in the game. All visual restraint in earlier zones earns this moment.
- The final white and silence before the end card should hold for longer than is comfortable.
