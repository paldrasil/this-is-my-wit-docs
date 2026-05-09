---
Status: Finalized
Owner: Design + Dev
Last Updated: 2026-05-09
Version: 0.3
Changelog:
  - Added metadata frontmatter.
  - Aligned agent rules with docs-only repository scope.
---

# Agent Guide

## Repository Scope
- This repository is docs-only.
- Allowed changes are limited to `docs/**`, `README.md`, and repository configuration files that support the documentation workflow.
- Do not add Unity runtime files, gameplay source code, generated builds, art assets, or implementation logs in this repository.

## Project Direction
- Target game: Unity top-down 3D stealth-puzzle prototype.
- This repository defines the design, milestone, and technical specifications for that game.
- Runtime implementation should happen only after the relevant milestone specs are finalized and in a repository/location that permits Unity project files.

## Working Rules

- Use [PLAN](./PLAN.md) as the project overview and [System Index](./system_index.md) as the documentation entry point.
- Follow the planning flow in [Working Conventions](../ai/conventions.md): `PLAN -> milestone spec -> implementation`.
- Keep documentation edits small, focused, and cross-linked.
- Update frontmatter (`Last Updated`, `Version`, `Changelog`) when changing a spec meaningfully.
- Do not run or require Unity build/test commands from this docs-only repository.
