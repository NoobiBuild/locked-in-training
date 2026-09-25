# Locked In — training progress in the browser

A small training companion from [NoobiBuilds](https://noobibuilds.co.za/). It brings a multi-week programme, workout videos and progress tracking into one browser interface.

This repository is an early implementation, shared as a source example. The [current website app](https://noobibuilds.co.za/Products/locked-in/) is a different build; this repository is not its current source release. It is not presented as a production-readiness assessment or a validated fitness programme.

## What the code contains

- Week and day navigation, workout completion and progress statistics.
- Weight entries and streak tracking.
- Embedded YouTube workout videos.
- Browser-local progress storage.
- JSON backup and restore.
- A service worker for caching selected resources.

The implementation is plain HTML, CSS and JavaScript. The main application lives in [index.html](index.html); the caching code is in [sw.js](sw.js). There is also an older duplicate application entry point in `locked-in-app/`. That copy needs a reference and deployment check before any removal. Use the repository root for the walkthrough below.

## Inspect it locally

With Python 3 installed, open a terminal in the repository root:

```sh
python -m http.server 8000 --bind 127.0.0.1
```

Then visit http://127.0.0.1:8000/. No package installation or build step is required by the current files.

On 25 September 2026, this entry point was served locally with Python 3 in an isolated browser. A synthetic weight entry survived reload after leaving the input field, and JSON backup export contained that value. This was a limited smoke check, not a full application test. Internet access is needed for YouTube playback and external resources.

## A useful walkthrough

Use sample entries rather than personal health information.

1. Open a week and inspect a day's workout.
2. Record sample progress and reload the page.
3. Export a backup.
4. In a separate browser profile, restore that backup and compare the recorded progress.

This is a suggested verification checklist, not a claim that automated tests have passed.

## Design choices and limits

**Local storage keeps the implementation small.** Progress belongs to the current browser and origin; there is no account-based synchronisation in this source. Clearing browser data can remove progress, so exports matter.

**Video playback depends on YouTube.** A service worker is present, but this does not establish full offline operation or offline video support. Cache updates and external-resource failures still need testing.

**Restore needs stronger validation.** The current implementation parses JSON and merges it into application state. It does not yet provide a complete schema check and reviewed restore workflow.

**The unlock flow runs in the browser.** It should not be treated as server-enforced access control or payment verification.

## Building and learning

This project belongs to an AI-assisted building practice: start with a practical problem, inspect what the tool produces, and refine the result until its behaviour and limitations are understandable. Repository ownership and generated code are not substitutes for explaining the decisions behind a build.

The next useful improvements are a verified walkthrough, clearer restore validation, a deliberate cache-update strategy and one maintained application entry point.

## Status and reuse

Documentation reviewed on 25 September 2026. Local startup, weight persistence and backup export were smoke-checked against the earlier public source. Restore displayed a success message, but final state comparison was interrupted by a browser-automation file-chooser issue. Cross-profile restore, malformed imports, workout completion, cache updates and offline operation remain unverified. Runtime reliability, adoption and fitness outcomes have not been established by this review. No automated test suite or licence file was present at that review. Public availability should not be interpreted as permission to redistribute; contact the owner about reuse.
