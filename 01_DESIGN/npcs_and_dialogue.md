# npcs_and_dialogue.md
## Ashenmoor — NPCs and Dialogue
**OUR NEW INDIE GAME STUDIO**
**Version:** 0.1
**Last Updated:** 2026-04-26
**Status:** Phase 0 — Stubs

---

## Document Conventions

Each NPC entry contains:
- **Role** — mechanical and narrative function
- **Location** — where they are found
- **Personality notes** — voice and register guidance for writing full dialogue
- **Conversation structure** — topic list with brief description of each branch
- **Key lines** — one or two lines that define the character's voice. These are locked — full dialogue should be written around them.
- **Flag dependencies** — which flags unlock or change dialogue options

Full dialogue scripts to be written in Phase 2 (Thornwall Build). These stubs are the brief for that writing.

---

## Thornwall Town NPCs

---

### Father Cassian
**Role:** Keeper of the Relic. Most complete account of the wizard's history. Gives the Relic freely.
**Location:** Church of the Pale Candle, vestry area.
**Personality:** Sixty, lean, white-haired. Carries genuine grief about the wizard's departure and genuine faith in the player's purpose once it is established.

**Conversation Topics:**
- *The town* — the fear, the shrine by the gate, the doubled watch. Atmospheric.
- *The wizard* — the most complete account available. The driving-out, Cassian's own regret. Unlocked after `ORVYN_SPOKEN`.
- *The Relic* — what it is, why he kept it, why he gives it. Transitions to Relic handoff.
- *The pool* — he knows of it. He will not say how. He says only that the water there is not natural water.

**Key lines:**
- ...

**Flag dependencies:**
- Topics *The wizard* and *The Relic* — require `ORVYN_SPOKEN` = true
- After `RELIC_ACQUIRED` — Relic topic replaced with brief farewell and blessing

---

### Maret
**Role:** Hedge-Witch. Exotic consumables vendor. Most direct source of information about the wraith and the dark pool.
**Location:** The Crooked Candle, down the side alley.
**Personality:** Ageless — could be forty or seventy. Seven rings, ink-stained fingers. Direct without being warm. The only person in town who does not seem surprised that a sorcerer's apprentice has arrived.

**Conversation Topics:**
- *Trade* — opens shop interface
- *The woods* — monitoring what is coming in from the north. Analytical rather than frightened.
- *The ruins / the pool* — she knows it is not natural water. Something is in it that was once a man. Will not say more until `RELIC_ACQUIRED`.
- *The wizard* — she respected him. Brief. Not sentimental.
- *The Hungering Branch* — offered freely after full conversation tree is exhausted.

**Key lines:**
- (about the wizard) *"Oh! Powerful wizard. Powerful wizard was he."*
- *"Something lives in the pool near the ruins. Something that was once a man."*
- *"Something of his will know when the time comes. You won't need to do anything. Just carry it."*

**Flag dependencies:**
- *The ruins* topic depth increases after `RELIC_ACQUIRED`
- `HUNGERING_BRANCH_UNLOCKED` — set after all Maret topics exhausted

---

### Brother Oswin
**Role:** Apothecary vendor. Secondary wizard lore source. Supply concerns add texture to the town's situation.
**Location:** The Green Mortar.
**Personality:** Former monk. Gentle, precise, quietly terrified. Managing his fear by becoming more organized.

**Conversation Topics:**
- *Trade* — opens shop interface
- *His supplies* — herb gatherers have stopped going into the woods. Practical worry.
- *The wizard* — knew him as a herbalist. Mentions the Relic obliquely — the priest has something of his.

**Key lines:**
- *"I cannot promise restocking. I'm telling you that now so it is not a surprise later."*

**Flag dependencies:**
- Relic mention plants the seed before Cassian confirms it — available from first meeting.

---

### Aldra
**Role:** Blacksmith vendor. Pragmatic anchor for the town.
**Location:** The Hammer Song, forge area.
**Personality:** Broad-shouldered, fifties, silver braid. Works longer hours than necessary because the sound of the hammer keeps people calm.

**Conversation Topics:**
- *Trade* — opens shop interface
- *The town's fear* — understandable and impractical in equal measure. Once, there were mighty knights for whom he forged weapons and armor, but where are they now?
- *The wizard* — came by occasionally for odd designs, all destroyed now.

**Key lines:**
- ...

**Flag dependencies:** None — full conversation available from first meeting.

---

### Hobb
**Role:** Tavern keeper and rumor hub.
**Location:** The Broken Antler tavern.
**Personality:** Heavyset, remarkable mustache, practiced calm. Has decided panic is bad for business and refuses to indulge it publicly.

**Conversation Topics:**
- *The tavern* — full every night. People who don't want to be alone at home.
- *Rumors* — overheard fragments. The couple from the northern road. The merchant and the standard. The guard and the wrong-walking shape.
- *The old soldier* — sits in the corner every night. Hobb can direct the player to him. The soldier sketches the castle layout if the player earns his trust.

**Key lines:**
- *"It's been like this three weeks. I've stopped asking people to go home. They don't want to go home."*
- *"See the old man in the corner? He hasn't talked to anyone in two months."*

**Flag dependencies:**
- Old soldier becomes interactive only after Hobb's direction

---

### Sela and Davan
**Role:** The rescued couple. Give the Bread and Salt. Davan's one line.
**Location:** Their home in the residential quarter.
**Personality:** Sela speaks. Warm, grateful, slightly embarrassed — she feels the gift is not enough. Davan is quiet in all prior interactions. He speaks once, here.

**Conversation Topics:**
- *Their home* — they are staying. No alternatives. No self-pity.
- *The gift* — Sela presses the Bread and Salt into the player's hands. No ceremony.
- *Davan's line* — a single sentence...

**Key lines:**
- Sela: *"..."*
- Davan: *[to be determined in full script — it lands.]*

**Flag dependencies:**
- `COUPLE_FOUND` — set on first conversation, triggers Bread and Salt gift

---

## Thornwall Castle NPCs

---

### King Orvyn
**Role:** Quest giver. Establishes stakes and reward.
**Location:** The Throne Room.
**Personality:** Perhaps sixty, grey-bearded, came to kingship from soldiering. Direct.

**Conversation Topics:**
- *The master* — went north three months ago. Has not returned. Told plainly.
- *The quest* — return with proof the Banished Lord has been slain. The reward will be significant.
- *The wizard* — the portrait is visible. If the player asks, Orvyn confirms it. An old friend. He says very little else.

**Key lines:**
- *"I am not going to tell you it will be safe. I am going to tell you it matters."*
- *"Come back. That is the first part of the reward."*

**Flag dependencies:**
- `ORVYN_SPOKEN` — set on completing this conversation

---

### Harwen
**Role:** Court physician. Gives healing items. Most fond of the wizard of all castle NPCs.
**Location:** The side corridor room.
**Personality:** Elderly, book-surrounded. Quietly and persistently angry about the wizard being driven off — carrying the injustice long past the point anyone else is still thinking about it.

**Conversation Topics:**
- *His work* — still doing it, regardless of everything.
- *The wizard* — treated him once for a sprained wrist. Best conversationalist in thirty years of court life. Gives the Tincts as a gesture, not a transaction.

**Key lines:**
- *"A sprained wrist, from moving too many bookshelves alone. We talked for four hours."*
- *"Take these. Come back."*

**Flag dependencies:** None.

---

### Emmet
**Role:** Young page. Atmospheric lore in motion. Most candid voice in the castle.
**Location:** Moving between the great hall and throne room corridor.
**Personality:** Twelve, gap-toothed, energy barely contained. Has been told to stay calm and finds this physically difficult.

**Conversation Topics:** (brief — Emmet is caught mid-errand)
- *The King* — hasn't laughed since the news came from the north.
- *Captain Mira* — sleeps in her armor now.
- *The wizard* — saw him turn a sparrow into a candle flame and back again.

**Key lines:**
- *"He turned a sparrow into a candle. Just to see if he could. Then he turned it back and it flew away and he looked very pleased with himself."*

**Flag dependencies:** None. Intercepting Emmet is optional.

---

## Wychfeld NPC

---

### Gest
**Role:** Optional NPC. Wolf patrol intelligence. Optional errand.
**Location:** Third farmhouse on the right, Amber Fields, barricaded inside.
**Personality:** Perhaps eighty. Refused to leave. Unbothered. Has been watching the wolves from her window for three weeks with the unsentimental precision of someone who spent sixty years farming. Makes excellent tea.

**Conversation Topics:**
- *Why she stayed* — she doesn't explain. It's obvious to her.
- *The wolves* — practical patrol intelligence. Useful to the player mechanically.
- *The errand* — something needed from a farmhouse two buildings north. Reward: Sorcerer's Salve.
- *The tea* — she offers it. No mechanical function. The player sits in a warm kitchen in a dead field and drinks tea with a very old woman who is not frightened.

**Key lines:**
- *"I've lived in this house for sixty-one years. I'm not leaving because the neighbors got strange."*
- *"They move in pairs mostly. The pair on the east side swings north every twenty minutes or so. You'll have a window."*

**Flag dependencies:**
- `GEST_ERRAND_COMPLETE` — unlocks full wolf intelligence and Salve reward

---

## Ambient / Non-Interactive NPCs

The following characters have limited or no dialogue trees. They exist as environmental detail.

**The Young Guard (red-haired)** — Thornwall gate. Makes eye contact. Does not speak beyond the initial entry exchange.

**Captain Mira** — Outer bailey, Thornwall Castle. A few lines if approached — military information, not a full tree. Asks about the woods. Does not sound like she believes the garrison is enough.

**Steward Aldric** — Great hall, Thornwall Castle. Functional dialogue only — intercepts the player, verifies identity, admits them to the throne room.

**The Old Soldier** — Corner table, the Broken Antler. Interactive only after Hobb's direction. Sketches the castle layout on a napkin after a short trust exchange. His map is partially accurate — things have changed since he was last inside. He does not say what happened to him there.

**The Water-Wraith** — Dark pool, outer ruins. Scripted exchange only — not a conversation tree. Recognition. The giving of the amulet. The drawing down. His face is visible above the waterline long enough to be seen clearly. He looks like a man who drowned a long time ago and has been waiting since.
