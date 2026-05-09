# Contributing (Docs-Only Repo)

## Scope
- This repository accepts documentation changes only.
- Allowed paths: `docs/**`, `README.md`, and repository config files for docs workflow.
- Do not add gameplay/runtime/source code files in this repository.

## Required flow
- Follow: `PLAN -> milestone spec -> implementation`.
- A milestone can start only after related game specifications are finalized.
- Keep links relative between docs whenever possible.

## Spec update requirements
- Update YAML frontmatter in edited specs:
  - `Last Updated`
  - `Version` (bump on meaningful changes)
  - `Changelog` (append concise bullet)

## Pull request checklist
- [ ] Changes are docs-only.
- [ ] Frontmatter updated for each changed spec.
- [ ] Relative links are valid.
- [ ] Change is reflected in relevant overview/spec index when needed.
