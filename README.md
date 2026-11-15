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

## Override the preset

A repository's `renovate.json` wins over the preset. Most fields replace the
preset's value; these merge with it instead:

| Field                 | Effect                                     |
| --------------------- | ------------------------------------------ |
| `packageRules`        | Appended after the preset's, so yours win. |
| `customManagers`      | Appended to the preset's managers.         |
| `addLabels`           | Adds to the preset's `labels`.             |
| `additionalReviewers` | Adds to the preset's `reviewers`.          |
