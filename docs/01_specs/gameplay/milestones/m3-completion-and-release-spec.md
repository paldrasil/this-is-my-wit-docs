---
Status: Draft
Owner: Design + Dev
Last Updated: 2026-05-28
Version: 0.1
Changelog:
  - Created M3 milestone spec for completion and release readiness.
  - Defined scope for win condition, objective tooltip, global whistle, grid-based sound, and WebGL build.
---

# M3 - Completion and Release Spec

## Goal
- Complete the playable loop with clear success feedback and release-ready build output.
- Lock behavior specs for win condition, objective guidance, global whistle response, and grid-based hearing.

## Scope
- Finalize milestone-level gameplay completion features on one vertical-slice map.
- Keep this milestone focused on behavior completion and release readiness.
- Exclude new content expansion, advanced polish, and post-launch balancing systems.

## Checklist tasks
- [ ] Win condition: buffalo reaches safe point `S` and the game shows win result state
- [ ] Current objective tooltip: player always sees the active objective for the current phase
- [ ] Whistle trigger all room: whistle affects the full map (all rooms), not only local room
- [ ] Sound detection migration: switch broad-phase sound query to grid-based lookup, without `Physics.OverlapSphere`
- [ ] WebGL build: produce a runnable WebGL build package with documented verification steps

## Task details

### 1) Win condition
- Define a single win rule for M3: main buffalo reaches safe point `S`.
- Require explicit win state transition and win-result UI path.
- Ensure win and lose are mutually exclusive terminal states in one run.

### 2) Current objective tooltip
- Add objective text tied to current loop phase (`Observe`, `Distract`, `Lead`, `Escape`).
- Update objective text on phase transition and major fail/retry transition.
- Keep tooltip language short, action-focused, and testable by state.

### 3) Whistle trigger all room (global)
- Whistle emits a map-wide acoustic event.
- Event reach is not constrained by room boundaries.
- AI reaction still follows each unit's priority/state rules; global trigger changes event scope only.

### 4) Grid-based sound detection
- Replace overlap-based broad-phase sound source scan with grid-cell query logic.
- Keep attenuation and threshold checks as hearing evaluation inputs.
- Preserve existing hearing semantics where possible while removing `Physics.OverlapSphere` dependency from broad-phase sound detection.

### 5) WebGL build
- Define target WebGL output profile for test release.
- Include required build artifacts and run instructions.
- Include a smoke-test checklist for load/start/restart and win/lose flow.

## Deliverables
- Updated gameplay behavior spec for completion-state loop (win/lose + objectives).
- Documented global whistle scope and grid-based hearing requirements.
- WebGL build readiness checklist with reproducible verification steps.
- M3 validation notes with pass/fail records for acceptance criteria.

## Dependencies and risks

### Dependencies
- M2 interaction flow remains stable enough to validate M3 end-state behavior.
- Phase/objective state model is available for UI tooltip mapping.
- Grid map/query services are available to support hearing broad-phase migration.
- Build environment supports Unity WebGL export and local browser smoke testing.

### Risks
- **State conflicts**: win/lose transitions may race if tiger catch and safe-goal entry happen in close timing windows.
- **Objective drift**: tooltip can become misleading if phase transitions are not centralized.
- **AI behavior regression**: global whistle may over-amplify reactions if unit-level filtering is not preserved.
- **Performance risk**: poorly optimized grid sound scans can regress frame time when many sources emit simultaneously.
- **Release mismatch**: WebGL build may run locally but fail on target host if artifact expectations are undocumented.

## Acceptance criteria
- Win triggers when the main buffalo reaches safe point `S`, and result UI shows win state in 3 consecutive runs.
- Lose triggers when tiger catch condition is met, and never overrides an already-committed win state in the same run.
- Current objective tooltip is visible during gameplay and updates correctly for each loop phase transition in 3 consecutive runs.
- Whistle emission is received across the full map regardless of room boundary; at least one valid target AI reacts from a different room in repeated tests.
- Broad-phase hearing detection path does not use `Physics.OverlapSphere` for sound-source discovery.
- Grid-based hearing query returns stable candidate sources and preserves threshold-based hearing outcomes in repeatable tests.
- WebGL build artifacts are generated successfully and pass smoke checks: load scene, start run, trigger lose, trigger win, and restart flow.

## Start gate
- This milestone is approved for implementation after:
  - This spec and linked references remain internally consistent with `PLAN` and `System Index`.
  - Owner confirms the M3 baseline map and target test scenarios used for acceptance verification.
  - WebGL target profile and smoke-test environment are documented before build verification starts.

## Related references
- [PLAN](../../../00_overview/PLAN.md)
- [System Index](../../../00_overview/system_index.md)
- [M2 - Interaction Complete Spec](./m2-interaction-complete-spec.md)
- [Vision Check](../feature/vision-check-spec.md)
- [Obstacle Generation](../feature/obstacle-generation-spec.md)
