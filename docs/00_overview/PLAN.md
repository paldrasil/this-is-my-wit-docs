---
Status: Draft
Owner: Design + Dev
Last Updated: 2026-05-28
Version: 0.4
Changelog:
  - Added metadata frontmatter.
  - Standardized milestone and tech-spec references.
  - Linked M3 milestone spec and updated milestone 3 scope.
---

# PLAN - This is my wit

Back to index: [System index](./system_index.md)

## 1) Player's objective
- Play as a buffalo herder and rely on wit instead of direct combat with the tiger.
- Control danger pacing using bait and sound distractions to open safe routes.
- Lead the buffalo herd (with priority on the main buffalo) to the safe point `S`.

## 2) Main game loop
- **Observe**: Read the tiger patrol route, perception zones, and terrain layout.
- **Distract**: Throw stones or place bait to push the tiger into `Investigate`/`Consume`.
- **Lead**: Use whistle to call the buffalo from a distance, then get close and use `lead` to make it follow.
- **Escape**: Use safe windows while the tiger is distracted to cross dangerous zones.
- Repeat this loop until the buffalo reaches the goal.

## 3) How to operate
- **Throw Stone**: Create noise to pull the tiger to an investigation point.
- **Drop Bait**: Lure the tiger into eating for a period of time and reduce long-range awareness.
- **Whistle**: Call the buffalo from a distance so it moves closer to the player.
- **Lead Buffalo (lead action)**: When the player is close to the buffalo, enable follow mode.
- **Release Lead**: The buffalo stops in place and no longer follows.
- **Tactical movement**:
  - Prefer `Tall Grass` and `Rock` for lower detection risk.
  - Avoid `Shallow Water` (noisy) and `Mud` (slow/sticky).
  - Buffalo cannot pass through `Deep Water` and `Cliff`.

## 4) Victory conditions and failure conditions
- **Victory**:
  - Buffalo reaches the safe point `S`.
  - Complete within target thresholds for detections/time (depending on mode).
- **Failure**:
  - Tiger enters `Chase` and catches the buffalo.
  - Player gets caught (if direct-fail mode is enabled).
  - Buffalo gets stuck and cannot be rescued within time/resource limits.

## 5) Difficulty level and progression
- **Level 1 (Tutorial)**:
  - One tiger, fewer high-risk obstacles, and a readable route.
  - Teaches core actions: stone, whistle, bait, and lead rope.
- **Level 2-3 (Core challenge)**:
  - Higher density of mud/shallow water and more complex patrol paths.
  - Requires tighter timing during tiger consume windows.
- **Level 4+ (Advanced stealth puzzle)**:
  - More choke points, less cover, and stronger terrain constraints on buffalo routes.
  - Limited bait/stone resources with high penalty for bad noise placement.
- **Progression systems**:
  - Unlock new maps, new AI patterns, and side goals (low noise, no detection, fast clear).

## 6) Visual direction
- Tactical top-down readability with fast situation parsing.
- Nature-driven palette: forest green, earth brown, stone gray; warning accents in yellow/red.
- Clear visual language by gameplay role:
  - `Tall Grass` and `Rock` read as safe/cover elements.
  - `Shallow Water` and `Mud` read as risky/noisy/slow zones.
  - `Deep Water` and `Cliff` read as non-traversable blockers.
- Concise VFX: sound ring on stone throw, tiger state icons (`Investigate`, `Consume`, `Chase`).

## 7) Technology stack
- **Engine**: Unity with a top-down 3D camera.
- **AI**: Tiger Finite State Machine (`Patrol`, `Investigate`, `Consume`, `Chase`) plus vision/hearing perception.
- **Pathfinding**: Grid-based A*/simple flow field for player, tiger, and buffalo.
- **Level data**: Tilemap plus scriptable data (or JSON) for fast tuning of vision, hearing, and consume timing.
- **Map pipeline**: Use TileWorldCreator for map blockout/generation in Unity, then tune gameplay per level.
- **Docs**: TileWorldCreator v4 documentation - https://giantgrey.gitbook.io/tileworldcreator-v4-documentation
- **Tech spec**: [3D asset pipeline](../01_specs/tech/3d-asset-pipeline.md) (3D asset integration pipeline for a team of 1 dev + 3 artists).
- **Tech spec**: [Evaluation loop](../01_specs/tech/evaluation-loop-spec.md) (continuous measurement and iteration loop for hard systems).
- **Audio**: Surface-based SFX (shallow water, mud, grass) for gameplay feedback.

## 8) Implementation milestones
- **M1 - Core prototype (1-2 weeks)**:
  - Detailed spec: [M1 core prototype spec](../01_specs/gameplay/milestones/m1-core-prototype-spec.md)
  - Grid movement for player/buffalo/tiger.
  - Basic tiger FSM plus vision/hearing detection.
  - Basic Win/Lose on one sample map.
- **M2 - Interaction complete (1 week)**:
  - Throw stone, drop bait, distance whistle, and lead/release all fully functional.
  - Tiger responds correctly to `Investigate`/`Consume`/`Chase`.
- **M3 - Level design pass (1-2 weeks)**:
  - Detailed spec: [M3 completion and release spec](../01_specs/gameplay/milestones/m3-completion-and-release-spec.md)
  - Finalize win condition, objective tooltip, global whistle behavior, and grid-based hearing.
  - Produce and validate a runnable WebGL build package.
- **M4 - Feedback & polish (1 week)**:
  - Minimal UI (objectives, alerts, failure states).
  - Core VFX/SFX and readability pass.
- **M5 - Playtest & balancing (continuous)**:
  - Track completion time, failure rate, and bottlenecks.
  - Tune AI perception, bait/stone economy, and map layout.
