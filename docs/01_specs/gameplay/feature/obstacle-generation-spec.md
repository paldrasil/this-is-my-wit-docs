---
Status: Draft
Owner: Design + Dev
Last Updated: 2026-05-19
Version: 0.3
---

# Obstacle Generation Spec

## Goal

Procedural environment obstacles per **room rig tile** (7×7 per room when `roomTile = 6`) that add tactical variation while keeping spawn areas clear. Playground visualizes obstacles as tag cubes only — no terrain tile writes.

## Playground workflow (current)

Implementation lives in **[`GridFlowPlayground`](../../../../this-is-my-wit-unity/Assets/Scripts/Playground/GridFlowPlayground.cs)** only:

- Shell map: `Cliff` + `Ground` + `Door` on `tileGrid` / `gridDetail` → TileWorldCreator layers (`Door` exports as ground).
- Per room: extract `roomTileGrid[7,7]` from global `tileGrid`, call [`ObstacleClusterGenerator.Generate`](../../../../this-is-my-wit-unity/Assets/Scripts/Generation/ObstacleClusterGenerator.cs); Water/Mud fill rig tiles on `tileGrid`/`gridDetail`; per cluster, detail cells on the **cluster contour** (4-neighbor outside the cluster footprint, outside rig not `Cliff`/`Door`) are set to `Ground`; Rock/Grass spawn as objects at tile center.
- Regenerate: clears `TagObjects/Spawns` and `TagObjects/Obstacles` before rebuild.

Production promotion (`GameManager`, `TileWorldCreatorService`) is a **later milestone**.

## Room rig layout

```
tx/ty:  0      1..5       6
        Cliff  Ground    Cliff
        Door on perimeter links (TileKind.Door)
```

Cluster growth uses **rig indices 0..6**. Only `TileKind.Ground` cells are placeable. `Cliff` and `Door` are skipped. Occupied rig cells cannot be reused by another cluster or type.

## API

**Input:** `TileKind[,] roomTileGrid` (7×7), [`ObstacleGenerationConfig`](../../../../this-is-my-wit-unity/Assets/Scripts/Generation/ObstacleGenerationConfig.cs), `Random`, optional `reservedTiles` (spawn rig coords).

**Output:** `List<ObstacleCluster>` — each cluster has `ObstacleKind` (`Water` | `Rock` | `Mud` | `Grass`) and `List<ObstacleClusterTile>` with `Tx`, `Ty` (rig coords).

**Generation order:** Water → Rock → Mud → Grass.

**World position:** `ObstacleClusterGenerator.TileCenterWorld(rigTx, rigTy, roomGlobalTileX, roomGlobalTileY, tileSize)`.

## Obstacle types (defaults)

| Type | Tag | Clusters / room | Tiles / cluster | Max tiles near Cliff/Door per cluster |
|------|-----|-----------------|-----------------|--------------------------------------|
| Water | `Water` | 0–2 | 1–4 | 1 |
| Rock | `Rock` | 2–5 | 1–2 | 1 |
| Mud | `Mud` | 1–4 | 1–3 | 1 |
| Grass | `Grass` | 3–7 | 2–5 | 1 |

A rig tile counts as **near Cliff/Door** when any 4-neighbor on `roomTileGrid` is `TileKind.Cliff` or `TileKind.Door`. After cluster growth, placements with more than the per-type max are rejected (same retry pattern as rock spacing).

Rock seeds enforce `minRockClusterSpacing` (Chebyshev, rig tiles).

## Reserved areas (rig tiles)

| Marker | Chebyshev radius from rig center `(roomTile/2, roomTile/2)` |
|--------|-------------------------------------------------------------|
| Player, Buffalo, Tiger | 1 |
| Stone, Bait | 1 |

Rooms without a spawn tag reserve nothing.

## Visual (playground)

Flat tag cubes under `TagObjects/Obstacles` — one cube per cluster tile at tile center world position (scale ~one 5×5 tile). No cluster/tile/cell hierarchy in v1.

## Out of scope (v1)

- Noise carve / detail cells
- `ObstaclePlacementMask` budgets
- Per-room BFS validation and global reachability

Can add carve + validation after cluster-on-rig is stable in playground.

## Related specs

- [M2 interaction milestone](../milestones/m2-interaction-complete-spec.md)
- [Vision check](vision-check-spec.md)
- [Evaluation loop](../../tech/evaluation-loop-spec.md)
