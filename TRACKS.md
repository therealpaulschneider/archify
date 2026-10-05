# Tracks in Archify

This public development fork includes the `interval` renderer, bounded label placement, shared Archify presentation, and opt-in diagram/JSON editing. It is based on upstream `9e35d2b0b39b155553ba9fcfe0b4f2a5198dd993`. Upstream maintainer agreement and integration with current main remain prerequisites for a final upstream PR.

## Setup and render

Use Node.js 22 and clone the Tracks branch:

```sh
git clone --branch paul/tracks https://github.com/therealpaulschneider/archify.git archify-tracks
cd archify-tracks/archify
npm ci
node bin/archify.mjs validate interval examples/storage.interval.json --json
node bin/archify.mjs deliver interval examples/storage.interval.json /tmp/storage-interval.html --json
```

Open the resulting standalone HTML in a browser. Append `?edit=1` to enable editing; download edited JSON and use it as the next CLI input. Changes in the browser do not overwrite your source file.

For agent use, load this checkout's [Archify skill](archify/SKILL.md). Use this checkout's CLI rather than an upstream installation without Tracks. The [authoring reference](archify/references/interval-tracks.md) links the schema and generic example and explains labels, arrows, coordinates, scaling, and validation. Tracks currently supports standard validation.

## Readability

Keep factual interval endpoints intact. Automatic placement tries interior positions, horizontal alternatives, and nearby external labels with leaders. Lane labels reserve a shared gutter; nearby guide captions may move while retaining a leader to their anchor. Inspect both light and dark themes and label ownership after rendering. Tall charts may scroll vertically; fitting an entire chart on screen does not take priority over readable text. The reader's font-size target is constrained by available viewport width.

## Contribution status

This fork is usable independently of upstream acceptance. Before an upstream PR is ready for final review, agree on the new type's scope with maintainers, integrate with current upstream main, and pass the relevant CI and package checks. Use the source checkout above to ensure you run this fork. Upstream installation links install upstream Archify, which does not include this contribution.

## Verification (2026-10-05)

- The broad local suite ran 1,522 tests: 1,464 passed, 56 were skipped, and two stale generated-artifact checks failed. Both artifacts were regenerated; the subsequent focused run passed all 56 tests, including those two checks. The complete suite was not rerun after regeneration.
- The canonical ZIP was rebuilt with Node 22.23.3; its extracted package passed the macOS package smoke check.
- Installed Google Chrome through Playwright passed light/dark Tracks rendering, horizontal-overflow, editor opt-in, and page-error smoke checks. These do not replace all skipped browser tests or human visual review.
- Upstream CI, other operating systems, and current-main integration remain unverified.
