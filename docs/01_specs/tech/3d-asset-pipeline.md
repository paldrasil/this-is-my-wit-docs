---
Status: Draft
Owner: Tech Art + Dev
Last Updated: 2026-05-08
Version: 0.3
Changelog:
  - Added metadata frontmatter.
  - Added Animator role and animation integration details.
---

# 3D Asset Integration Pipeline (Unity Top-Down 3D)

## 1) Scope and goals
- Create a clear 3D asset integration pipeline for 1 dev and 3 3D artists.
- Ensure assets enter the game quickly with strong gameplay readability and performance.
- Reduce bottlenecks between dev and art through small-batch, short-loop handoffs.

## 2) Team roles
- **Dev (Unity Integration Owner)**:
  - Import asset, setup prefab/material/collider/nav.
  - Integrate into gameplay scenes and verify logic/performance.
  - Consolidate technical feedback for artists.
- **Animator**:
  - Rig and animate tiger, buffalo, and player based on gameplay needs.
  - Deliver animation clips, avatar/rig mappings, and transition notes.
  - Work with dev on Animator Controller setup, blending, and in-game tests.
- **Artist A (Environment)**:
  - Ground modules, terrain sets, cliffs, rocks, and primary foliage.
- **Artist B (Creatures/Characters)**:
  - Buffalo, tiger, player models, and required variations.
- **Artist C (Props/Set Dressing)**:
  - Gameplay props (bait, stone pile, markers) and set-dressing props.

## 3) Asset priority
- **P0 - Gameplay critical**:
  - Ground, tall grass, rock, mud, shallow/deep water, cliff blockers.
  - Tiger, buffalo, player proxy.
  - Core animation clips: idle, move, alert/chase, basic interactions.
- **P1 - Readability support**:
  - Interactive props, state visual markers, and basic environment variations.
- **P2 - Polish**:
  - Hero props, decals, extra foliage, and ambience details.

## 4) Technical standards
- Use one consistent scale, unit, axis, and forward direction across all assets.
- Set pivots based on gameplay needs (grounding, rotation, grid snapping).
- Keep naming consistent by group: `env_`, `char_`, `prop_`, with type and variation suffixes.
- Use one shared material/shader pipeline in the Unity project.

## 5) Folder and handoff structure
- **Source art**: organize by `environment`, `characters`, `props`.
- **Unity import**:
  - `Art/Models/Environment`
  - `Art/Models/Characters`
  - `Art/Animations/Characters`
  - `Art/Models/Props`
  - `Art/Materials`
  - `Art/Textures`
  - `Prefabs/Environment`
  - `Prefabs/Characters`
  - `Prefabs/Props`
- Each handoff must include a checklist: asset list, intended use, collider notes, known issues.

## 6) Integration workflow (weekly loop)
1. Artists hand off asset packs by priority P0/P1/P2.
2. Dev imports into Unity and validates scale/pivot/material basics.
3. Dev creates prefabs and assigns colliders plus nav areas/tags by gameplay type.
4. Set up Animator Controller and map clips to gameplay states.
5. Place in test maps and verify readability with top-down camera.
6. Finalize quick feedback and iterate in the next loop.

## 7) TileWorldCreator map workflow
- Use TileWorldCreator for fast map blockout/generation.
- After map generation:
  - Export/convert into Unity-scene-compatible data.
  - Assign prefabs by tile groups (ground/cover/risk/blocked).
  - Hand-tune choke points, patrol routes, and stealth spaces.
- Any major gameplay change must update mapping rules to prevent drift between generator output and final scenes.

Reference docs: [TileWorldCreator v4 Documentation](https://giantgrey.gitbook.io/tileworldcreator-v4-documentation)

## 8) Definition of done per asset
- Correct scale, pivot, and naming.
- Error-free import with correct material/shader rendering.
- Gameplay-ready prefab exists in Unity.
- Animation clips import cleanly and transition correctly in Animator Controller.
- Collider/nav setup matches intended behavior.
- Tested in real gameplay scenes with top-down 3D camera.

## 9) Risks and mitigations
- **Risk**: Assets look good but are hard to read from top-down camera.
  - **Mitigation**: Test directly in gameplay scenes; prioritize silhouette and value contrast.
- **Risk**: Heavy assets reduce performance.
  - **Mitigation**: Enforce poly/texture budgets, LOD usage, and material reuse.
- **Risk**: Dev is blocked while waiting for final assets.
  - **Mitigation**: Use proxy prefabs first, lock interfaces early, swap final assets later.

## 10) Milestone alignment
- **M1**: Full 3D proxy coverage for end-to-end gameplay loop.
- **M2**: P0 complete and technical integration standards locked.
- **M3**: P1 complete, readability pass.
- **M4**: P2 + optimization pass.
- **M5**: Content lock, bugfix, final build.
