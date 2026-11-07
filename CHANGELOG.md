# Changelog

## [Unreleased]

## [0.1.1] - 2026-11-07

- `index.csv` lists every PyPI project above serial 32,000,000, sorted by serial,
  with the columns of `projects.csv`. The serial in `marks.json` points into it.
- The Sync workflow runs `sync` every hour. The Harvest workflow runs `walkdown`,
  `catchup`, and `backfill` four times an hour. Both run on demand too, and push
  their commits to `main`.

## [0.1.0] - 2026-11-05

First release: `projects.csv`, with the columns the README lists.
