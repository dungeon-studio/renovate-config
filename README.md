<!-- SPDX-FileCopyrightText: 2026 Alex Brandt <alunduil@gmail.com> -->
<!-- SPDX-License-Identifier: MIT -->

# `renovate-config`

Shared Renovate preset for Dungeon Studio's repositories.

## Use the preset

Install the [Renovate GitHub app](https://github.com/apps/renovate) on the
repository, then extend the preset from `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>dungeon-studio/renovate-config"]
}
```

Add only repository-specific settings beside `extends`.

## Automerge updates

The `automerge-minor` preset merges minor, patch, pin, and digest
updates, and lock file maintenance, once required checks pass. Extend
it beside the default preset:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>dungeon-studio/renovate-config",
    "github>dungeon-studio/renovate-config:automerge-minor"
  ]
}
```

Extend it only when the branch ruleset lets Renovate merge and its
required checks catch a broken dependency update. Renovate merges once
required checks pass, whatever other checks report, so without
required checks an update merges untested.

These updates still wait for review:

- Majors.
- Updates from a 0.x version.
- Other updates the versioning scheme marks as breaking.
- Updates in `.github/workflows/release.yml` and `.github/actions/**`,
  other than runner images, because a release job runs them beside its
  publishing credential.

To stop automerging, remove the preset from `extends`.

## Override the preset

A repository's `renovate.json` wins over the preset. Most fields replace the
preset's value; these merge with it instead:

| Field                 | Effect                                     |
| --------------------- | ------------------------------------------ |
| `packageRules`        | Appended after the preset's, so yours win. |
| `customManagers`      | Appended to the preset's managers.         |
| `addLabels`           | Adds to the preset's `labels`.             |
| `additionalReviewers` | Adds to the preset's `reviewers`.          |
