<!-- SPDX-FileCopyrightText: 2026 Alex Brandt <alunduil@gmail.com> -->
<!-- SPDX-License-Identifier: MIT -->

# Agent instructions for `renovate-config`

Document behaviour that consuming repositories see in
[`README.md`](README.md).

## Presets

- Each root JSON file is a preset. Other repositories extend it as
  `github>dungeon-studio/renovate-config:<name>`, or without the suffix
  for `default.json`. Renaming or removing one breaks every repository
  that extends it.
- Renovate reads presets from `develop`. Consumers, including this
  repository, see a preset change only after it merges.
- In `automerge-minor.json`, set automerge on the top-level update-type
  objects, outside `packageRules`. Renovate applies `packageRules` last,
  so the release-workflow hold in `default.json` still wins.
- `gitIgnoredAuthors` takes the bot's user ID from
  `gh api users/<bot>[bot]`.
- `default.json` mirrors the `default.json` in `alunduil/renovate-config`
  without extending it. Port upstream changes by hand, keeping the
  `description` texts that differ on purpose.

## Hooks and CI

- Run hooks with `prek run --all-files`, with the `mise.toml` tools
  active. The Vale hooks run whichever Vale is on `PATH`.
- Use only actions on the organization's Actions allowlist, which
  dungeon-studio/dungeon-studio-infrastructure manages.
