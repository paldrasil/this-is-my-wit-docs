---
Status: Finalized
Owner: Gameplay Dev
Last Updated: 2026-05-09
Version: 0.4
Changelog:
  - Added metadata frontmatter.
  - Kept M1 scope/checklist aligned with PLAN.
  - Added dependencies, risks, start gate, and measurable acceptance criteria.
---

# M1 - Core Prototype Spec

## Goal
- Build an end-to-end playable prototype on one sample map.
- Validate the core gameplay loop: movement, tiger avoidance, buffalo leading, and basic win/lose.

## Scope
- Focus only on core features to validate gameplay feasibility.
- Use simple/proxy assets (capsules for characters) to prioritize gameplay logic.
- Exclude final art, advanced UI, multi-level progression, balance tuning, and production-ready animation.
- Use this spec as the execution contract for M1 after the Unity implementation repository/location is confirmed.

## Checklist tasks
- [ ] Init project
- [ ] Use capsules for Tiger, buffalo, and player
- [ ] Create simple map use TileWorldCreator
- [ ] Grid movement for player/buffalo/tiger
- [ ] Basic tiger FSM + vision/hearing detection
- [ ] Basic Win/Lose on one sample map

## Start gate
- This milestone is approved for implementation after:
  - This spec remains `Status: Finalized`.
  - The implementation location is confirmed as a Unity project repository or folder that permits runtime/source files.
  - The sample map coordinate convention is documented in the game concept or implementation notes before grid/pathfinding work starts.
  - Design and dev agree that M1 uses proxy visuals and prioritizes behavior validation over polish.

## Task details

### 1) Init project
- Create a Unity top-down 3D project using the current folder standards.
- Set up a sample scene for gameplay prototyping.
- Prepare basic input, top-down camera, and minimal gameplay bootstrap loop.

### 2) Use capsules for Tiger, buffalo, and player
- Use capsule/proxy objects to represent the 3 actors: Tiger, Buffalo, Player.
- Assign colors/labels so each actor is easy to distinguish in test scenes.
- Attach colliders and basic movement components.

### 3) Create simple map use TileWorldCreator
- Build a small map with a simple layout to test the core loop.
- Include basic zones: paths, blockers, risk areas, and a safe goal.
- Block out the map using TileWorldCreator, then hand-tune key gameplay points.

### 4) Grid movement for player/buffalo/tiger
- Implement grid movement for Player, Buffalo, and Tiger.
- Ensure stable movement, no clipping through blockers, and correct input response.
- Buffalo can either hold position or follow based on basic gameplay rules.

### 5) Basic tiger FSM + vision/hearing detection
- Minimal tiger FSM: `Patrol`, `Investigate`, `Consume`, `Chase`.
- Prototype-level vision/hearing detection with priority on correct behavior over high fidelity.
- Add simple debug visualization (gizmo/log) for quick AI state testing.

### 6) Basic Win/Lose on one sample map
- Win: buffalo reaches the safe destination on the sample map.
- Lose: tiger catches the buffalo or player (based on prototype rules).
- Show minimal win/lose feedback (UI text/log/quick restart).

## Deliverables
- One playable prototype scene.
- One sample map that supports full win/lose loop testing.
- Core gameplay scripts for movement, tiger FSM, and win/lose.
- Short M1 test notes recording the tested scene, pass/fail result, and any known prototype limitations.

## Dependencies and risks

### Dependencies
- Unity project location that allows `Assets/`, `Packages/`, `ProjectSettings/`, and generated Unity metadata.
- Unity version selected before project initialization.
- TileWorldCreator availability, licensing, and compatible Unity version confirmed before map blockout.
- Coordinate convention for grid cells confirmed before movement, pathfinding, and patrol data are implemented.
- Basic input scheme selected for prototype movement and interactions.

### Risks
- **TileWorldCreator setup delay**: If setup blocks M1, use a hand-built proxy grid for the sample map and keep TileWorldCreator integration as a follow-up task.
- **Coordinate mismatch**: If row/column and world-space axes are not defined early, patrols and paths may behave incorrectly. Mitigate by documenting the convention and adding visible grid debug labels.
- **AI scope creep**: Tiger behavior can expand quickly. Limit M1 to the four required states and debug-visible transitions.
- **Pathfinding complexity**: Full production pathfinding is not required for M1. Use the simplest grid A* or waypoint approach that validates the loop.
- **Ambiguous pass/fail behavior**: Keep win/lose, detection, and interaction criteria measurable so test runs can be repeated consistently.

## Acceptance criteria
- The prototype runs in one M1 sample scene for 3 consecutive manual test runs without soft locks, crashes, or actors leaving the playable grid.
- Player, buffalo, and tiger move one grid cell at a time and cannot enter cells marked as blockers for that actor.
- The buffalo has at least two observable modes: `HoldPosition` and `FollowPlayer`; releasing the lead returns the buffalo to `HoldPosition` within 1 input action.
- Whistle moves or pathfinds the buffalo toward the player when the buffalo is within the configured whistle range, and does nothing when outside that range.
- A stone/noise trigger moves the tiger from `Patrol` to `Investigate` and sends it to the noise location in at least 3 repeated tests.
- A bait trigger moves the tiger to `Consume` for a visible timed window, then returns it to patrol/investigation behavior after the timer ends.
- Tiger vision or near detection moves the tiger to `Chase` when the player or buffalo enters the configured detection area in at least 3 repeated tests.
- Win condition triggers only when the buffalo reaches the safe destination `S`.
- Lose condition triggers when the tiger catches the buffalo; player-caught failure may be enabled only if documented in the test notes.
- The sample map can be completed from start to win in 3 consecutive manual runs using the intended core loop: observe, distract, lead, escape.
