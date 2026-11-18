<!-- SPDX-FileCopyrightText: 2026 Alex Brandt <alunduil@gmail.com> -->
<!-- SPDX-License-Identifier: MIT -->

# Agent instructions for renovate-config

Repository rules for every coding agent. Claude Code reads
[`CLAUDE.md`](CLAUDE.md), which imports this file. Usage and override
semantics for consumers live in [`README.md`](README.md).

## Presets

- Every JSON file at the root is a preset that consuming repositories
  extend as `github>dungeon-studio/renovate-config:<name>`; `default.json`
  is the bare `github>dungeon-studio/renovate-config`. Renaming or removing
  one breaks every repository extending it.
- Renovate resolves presets from `develop`, so a preset change reaches
  consumers, this repository included, only after it merges.
- JSON carries no comments. Put each rule's reason in its `description`.
- Keep the update-type blocks in `automerge-minor.json` (`"minor": {
  "automerge": true }` and siblings) outside `packageRules`. Renovate
  applies `packageRules` after update-type config, and that order keeps the
  release-workflow hold in `default.json` in force.
- `gitIgnoredAuthors` takes the bot's user ID from
  `users/<bot>[bot]`, not its GitHub App ID.
- `default.json` started as a copy of alunduil/renovate-config's
  `default.json` and doesn't extend it. Port upstream changes by hand; some
  `description` texts differ on purpose.

## CI and branches

- Branch rulesets in dungeon-studio/dungeon-studio-infrastructure require
  the jobs `Run pre-commit hooks` and `Check Git flow source branch` by
  name. Keep those job names.
- An action a workflow uses must be on the organization's Actions
  allowlist, which dungeon-studio/dungeon-studio-infrastructure manages.
- Target pull requests at `develop`. Only `release/*` and `hotfix/*`
  merge into `main`.

## Hooks

Run hooks with `prek run --all-files`. mise pins prek, Node, and Vale in
`mise.toml`; the Vale hooks are `system` hooks and need that Vale on
`PATH`.
