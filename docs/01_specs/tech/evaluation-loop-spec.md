---
Status: Draft
Owner: Gameplay + QA
Last Updated: 2026-05-08
Version: 0.3
Changelog:
  - Added metadata frontmatter.
  - Defined evaluation metrics and quality gates for iterative balancing.
---

# Evaluation Loop Tech Spec

## 1) Purpose
- Some game systems cannot be solved correctly with one implementation pass.
- Instead of guessing the "right answer" up front, the team runs a continuous **build -> evaluate -> improve** loop.
- The goal is to make decisions from measured data, not intuition alone.

## 2) Problem classes in scope
- Enemy AI behavior
- Difficulty curve
- Map generation
- Hit detection
- Score calculation
- Automatic puzzle generation
- Game balance

## 3) Evaluation loop model
1. **Define target**: set quantitative targets for each system (AI, map, performance, UX).
2. **Create evals**: write scripts/tests plus verification artifacts to measure current quality.
3. **Run baseline**: execute against current build to establish baseline metrics.
4. **Implement change**: update logic/parameters/content.
5. **Re-run evals**: measure again under the same conditions.
6. **Compare and decide**: keep changes if improved/passing; rollback or iterate if degraded.
7. **Log results**: store run results to track long-term trends.

## 4) Evaluation metrics for this project
- **Completion Rate**:
  - Percentage of players completing a level/map.
  - Used to evaluate overall gameplay-loop viability.
- **Average playtime**:
  - Average time to complete or fail.
  - Used to validate pacing and level length.
- **Frequency of clashes with the enemy**:
  - Number of enemy encounters or detections per run.
  - Used to measure stealth pressure and AI behavior.
- **FPS decrease**:
  - FPS drop in heavy scenes (many AI, dense map objects, high VFX load).
  - Used to control performance regressions.
- **Reachability of generated maps**:
  - Percentage of generated maps with at least one valid path from spawn to goal.
  - Used to validate map generation quality.
- **Success rate by difficulty level**:
  - Win rate at each difficulty tier.
  - Used to tune difficulty curve and game balance.
- **Checking for overlapping UI elements**:
  - Percentage of screens with UI overlap issues.
  - Used to verify readability and UX consistency.

## 5) Evaluation artifacts
- **Eval scripts**:
  - Simulation/replay scripts for automatic metric collection.
  - Static checks for map quality (reachability/connectivity) and UI overlap.
- **Verification artifacts**:
  - Per-run JSON/CSV logs.
  - Screenshot/frame capture or short replay for failed cases.
  - Summary report: baseline vs current.
- **Scenario sets**:
  - Fixed map seed set for fair comparisons.
  - Standard scenario set for AI, hit detection, and puzzle systems.

## 6) Quality gates (suggested)
- Do not merge if completion rate drops below accepted threshold.
- Do not merge if FPS regression exceeds the performance budget.
- Do not merge if generated-map reachability drops significantly.
- Do not merge if UI overlap appears on target resolutions.
- If one metric degrades, include a reason and next-iteration recovery plan.

## 7) Execution cadence
- **Per PR (fast pass)**:
  - Run smoke evals for core metrics: FPS, reachability, UI overlap.
- **Daily build**:
  - Run full evals on the standard scenario set.
- **Milestone review**:
  - Review metric trends by week/milestone.
  - Rebalance AI, difficulty, and map rules based on evidence.

## 8) Roles and responsibilities
- **Gameplay dev**:
  - Build and maintain eval scripts for AI, difficulty, score, and puzzle systems.
- **Technical design/game design**:
  - Set target metrics, pass/fail thresholds, and tuning decisions.
- **QA/Producer (or test owner)**:
  - Ensure scheduled eval runs, track regressions, and consolidate reports.

## 9) Implementation phases
- **Phase 1 - Baseline instrumentation**:
  - Add baseline telemetry for completion, playtime, clash frequency, and FPS.
- **Phase 2 - Automated evals**:
  - Automate map reachability, difficulty-tier success rate, and UI overlap checks.
- **Phase 3 - CI integration**:
  - Integrate quality gates into build/PR pipeline.
- **Phase 4 - Continuous tuning**:
  - Use eval results as required input for each gameplay balancing cycle.

## 10) Expected outcomes
- Reduce blind trial-and-error during AI/map/difficulty tuning.
- Catch regressions early before late milestone stages.
- Establish a repeatable, measurable improvement loop that scales with project scope.
