---
Status: Draft
Owner: Design + Dev
Last Updated: 2026-05-11
Version: 0.2
Changelog:
  - Aligned M2 to prototype-friendly scope format.
  - Locked vertical-slice flow and unified Throw action for stone/bait.
---

# M2 - Interaction Complete Spec

## Goal
- 1 full loop test map to validate the interaction-complete gameplay loop in prototype quality.

## Scope
- Vertical slice on one test map with 3 phases:
  - Phase 1: player finds buffalo, collects limited tools (stone/bait), tiger starts in low alert/sleeping setup.
  - Phase 2: player uses whistle and lead to start buffalo movement, tiger wakes and begins active response.
  - Phase 3: player creates safe windows with throw actions while crossing risky terrain.
- Interactions are playable end-to-end: `Throw` (stone/bait), distance whistle, and lead/release.
- `Drop Bait` uses the same `Throw` action flow as stone, but with bait payload and `Consume` outcome.
- Tiger response priorities are clear for prototype behavior: `Chase` > `Consume` > `Investigate` > default patrol.
- Terrain behavior included for this milestone: `Tall Grass`, `Shallow Water`, `Mud`.
- Surface-based sound model (medium fidelity):
  - Actions/footsteps emit base intensity `n` by surface/event type.
  - Intensity attenuates by distance.
  - Tiger hears events when received intensity >= threshold `x`.
  - Covered sources: footsteps on terrain, whistle, and throw impact on terrain.

## Checklist tasks
- [ ] Design test map layout for 3-phase vertical slice flow
- [x] Phase 1 map setup: buffalo in mud zone, tool pickup routes (stone/bait), low-alert tiger start
- [x] Phase 2 map setup: whistle-to-lead transition zone and tiger wake trigger area
- [ ] Phase 3 map setup: high-tension crossing with risky terrain and throw-based distraction windows
- [x] Pickup interaction for `stone` and `bait` on map
- [x] Grid pathfinding with obstacle avoidance stable on test map
- [x] Terrain interactions: `Tall Grass`, `Shallow Water`, `Mud`
- [x] Unified `Throw` action: stone and bait share action flow
- [x] Tiger response verified: `Investigate` (stone/noise), `Consume` (bait), `Chase` (threat)
- [ ] Distance whistle + lead/release loop playable end-to-end in one map
