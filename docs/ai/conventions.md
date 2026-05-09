---
Status: Finalized
Owner: Design + Dev
Last Updated: 2026-05-08
Version: 0.3
Changelog:
  - Added status/versioning and cross-link conventions for all docs.
---

# Working Conventions

## 1) Planning flow
- All implementation work must follow: `PLAN (overview)` -> `Milestone Spec (execution)` -> `Implementation`.
- `PLAN` defines goals, scope, tech direction, and milestones at overview level.
- Each milestone listed in `PLAN` must have a corresponding detailed spec before work starts.

## 2) Milestone spec requirements
- Each milestone spec must include at minimum:
  - Goal and scope
  - Clear task checklist
  - Deliverables
  - Acceptance criteria
  - Dependencies and risks (if any)
- The milestone spec is the source of truth for execution in that milestone.

## 3) Game design spec policy
- Game design specs can be expanded incrementally by milestone; they do not need full detail upfront.
- Before a new milestone begins, update related game design sections (rules, balancing targets, intended experience, test cases).
- Any game design change during a milestone must be reflected back into the corresponding milestone spec.

## 4) Start gate rule (mandatory)
- **A milestone may start only after the game specifications are finalized.**
- "Finalized" means:
  - The spec has a clear current version.
  - Checklist and acceptance criteria are approved.
  - Key stakeholders (design + dev owner) confirm execution readiness.
- Do not start implementation while the spec remains draft/unapproved.

## 5) Change control
- If major scope changes happen during an active milestone:
  - Update the spec first
  - Mark the change (change note)
  - Re-confirm acceptance criteria
- Avoid coding first and documenting later.

## 6) Traceability
- `PLAN` must reference related milestone specs.
- Milestone specs should reference back to `PLAN` and supporting tech/gameplay specs.
- Important decisions must leave traceable documentation so the team can audit quickly.

## 7) Status and versioning (inside each doc)
- Use YAML frontmatter at the top of each committed spec:

```yaml
---
Status: Draft
Owner: TBD
Last Updated: YYYY-MM-DD
Version: 0.1
Changelog:
  - Short bullet describing what changed.
---
```

- Bump **`Version`** (for example `0.1` -> `0.2`) when the document changes meaningfully.
- Append **`Changelog`** bullets; do not rely on filename suffixes for versions.

## 8) Cross-links
- Prefer **relative** Markdown links between specs (for example from `gameplay/combat/damage_pipeline.md` to `../progression/stats.md`).
- Use [System index](../00_overview/system_index.md) as the documentation entry point.
