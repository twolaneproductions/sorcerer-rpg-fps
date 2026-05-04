# tech_overview.md

- [tech\_overview.md](#tech_overviewmd)
  - [Ashenmoor — Technical Overview](#ashenmoor--technical-overview)
  - [Engine](#engine)
  - [Platform Targets](#platform-targets)
  - [Architecture Overview](#architecture-overview)
  - [Version Control](#version-control)
  - [Build Pipeline](#build-pipeline)
  - [Performance Targets](#performance-targets)
  - [Known Technical Risks](#known-technical-risks)


## Ashenmoor — Technical Overview
**OUR NEW INDIE GAME STUDIO**
**Version:** 0.1
**Last Updated:** 2026-04-26
**Status:** Phase 0 — Draft

---

## Engine

**UZDoom**
UZDoom is an open-source, actively maintained source port of the original Doom engine with modern rendering capabilities, a robust scripting language (ZScript), and native cross-platform support. It was chosen for the following reasons:

- **First-person combat foundation** — movement, hit detection, and weapon behavior are battle-tested and require no custom implementation
- **ZScript depth** — sufficient for NPC dialogue systems, quest flag management, inventory logic, and save state handling without requiring a general-purpose engine
- **Heretic / Hexen precedent** — the engine has a documented history of supporting fantasy FPS games with magic weapons and non-standard mechanics
- **No licensing cost** — appropriate for a minimal-budget two-person project
- **Community knowledge base** — large existing modding community with documented solutions to common implementation challenges

**Engine version to be locked at project start and documented in `decision_log.md`. Do not update mid-production.**

---

## Platform Targets

| Platform | Status | Notes |
|---|---|---|
| Windows (PC) | Primary | Target for all development and testing |
| Mac | Secondary | UZDoom native support — verify at alpha |
| Linux | Secondary | UZDoom native support — verify at alpha |
| Console | Out of scope | Not in initial release |

**Distribution:** itch.io for initial release. Steam under consideration for post-launch if reception warrants.

---

## Architecture Overview

UZDoom's architecture handles the following natively — no custom systems required:

- First-person movement and collision
- Projectile physics and hit detection
- Basic enemy AI states (patrol, detect, attack, death)
- Audio playback and spatialization
- Level loading and zone transitions

The following require custom ZScript implementation:

- **NPC dialogue system** — branching conversation trees with quest flag triggers
- **Inventory and equipment system** — weapon slots, armor slots, consumable stacking
- **Quest flag manager** — tracks player progress through the main spine and optional content
- **Shop system** — item purchase interface for Thornwall vendors
- **Moat swim sequence** — disorientation mechanic, directional ambiguity, air timer
- **HUD customization** — health, mana, active consumable display in period-appropriate aesthetic
- **Save system** — checkpoint-triggered autosave at three defined locations

---

## Version Control

**Tool:** Git
**Repository:** Private — hosted on GitHub

**Branch structure:**
- `main` — stable, always-releasable builds only
- `dev` — active development, merged to main at each phase milestone
- `feature/[name]` — individual feature branches, merged to dev when complete

**Commit conventions:**
- Present tense, imperative: *Add dialogue tree for Father Cassian*, not *Added* or *Adding*
- Prefix with system tag: `[dialogue]`, `[combat]`, `[inventory]`, `[level]`, `[audio]`, `[ui]`
- No commit to main without both team members reviewing

**Asset handling:**
Large binary assets (textures, audio files, WAD resources) tracked via Git LFS. Raw source files kept in a shared cloud folder outside the repository. Only compiled/optimized assets commit to the repo.

*Full branching and merge procedure in: [version_control.md](./version_control.md)*

---

## Build Pipeline

A working build is a UZDoom-loadable WAD or PK3 file produced from the current dev branch. Both team members must be able to produce a build independently.

**Build steps:**
1. Pull latest from `dev`
2. Compile ZScript — errors must be zero before proceeding
3. Package assets into PK3 structure
4. Launch via UZDoom with project config file
5. Confirm title screen loads without error
6. Log build date and branch state in `decision_log.md`

Builds are produced at the end of every phase and shared externally with designated playtesters.

---

## Performance Targets

| Metric | Target |
|---|---|
| Frame rate | 60fps minimum |
| Resolution | 1080p native |
| Load times | Under 5 seconds per zone transition |
| Minimum hardware | Mid-range PC circa 2018 |

UZDoom's rendering overhead is low by modern standards. These targets should be achievable without aggressive optimization provided asset complexity is kept in check — appropriate for a one-hour game's scope.

---

## Known Technical Risks

**Moat swim sequence** — The disorientation mechanic (surface is not up, air timer, directional ambiguity) has no direct UZDoom precedent. Requires early prototyping in Phase 1 to confirm feasibility. If it cannot be implemented satisfactorily within UZDoom's constraints, a simpler flood-room traversal sequence is the fallback.

**Dialogue system complexity** — Branching NPC dialogue with quest flag integration is implementable in ZScript but represents the most custom code in the project. Allocate disproportionate early development time here — it underpins the entire town section.

**Save system** — UZDoom's native save is full game-state. A checkpoint-only autosave system that restricts player access to manual saving requires custom implementation. Research this constraint early.
