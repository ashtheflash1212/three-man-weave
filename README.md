# Five-Man Weave

A turn-based, browser-playable NBA card battle game. Draft a five-man starting lineup from a
pool of real historical NBA players, then go head-to-head with an offense/defense play-calling
system resolved by a custom ratings-driven shot-odds engine.

Runs as a single self-contained `index.html` — no build step, no server required to play solo.

## Play it

Just open `index.html` in a browser.

## Features

- **Draft mode** — pick one of five randomly-pooled candidates per roster slot (PG/SG/SF/PF/C)
  from a modeled dataset of 455 real historical NBA players, each rated across 25 skill
  attributes.
- **Turn-based play-calling** — 8 offensive actions vs. 5 defensive calls, resolved by a shot-odds
  engine that factors in the matchup, fatigue, double-teams, and momentum. Free throws on shooting
  fouls resolve independently of the field-goal result.
- **Abilities & upgrades** — 10 archetype-based player abilities (passives + once-per-game moves)
  plus a 3-tier in-game upgrade system.
- **Multiplayer** — real-time 1v1 over Firebase Firestore, with a host/guest room-code flow,
  deterministic seeded RNG so both clients resolve a turn identically, and mid-game resume.
- **Collection mode** — a card-collection meta-game with its own currency and drop odds.
- **Tutorial** — a fully scripted, auto-playing walkthrough (draft pick + a full battle round)
  with animated cursor movement and step navigation.
- **Audio** — a two-layer sound system: a hand-built Web Audio API synthesizer for procedural
  sound effects, layered with a separate recorded-clip player, both sharing one mute/volume
  control. All recorded clips are loudness-matched.

## Tech stack

- Vanilla JavaScript, HTML5, CSS — no framework, no bundler
- Web Audio API for synthesized sound
- Firebase Firestore for multiplayer sync and cloud collection saves
- Playwright (Node.js) for automated functional/regression testing during development

## Notes

- `audio/` holds the original source clips used to build the in-game sound effects; the actual
  clips the game plays are embedded directly in `index.html` as base64 data URIs, so nothing here
  needs to be loaded separately at runtime.
- Multiplayer requires a Firebase project (see `FIREBASE_CONFIG` near the top of the multiplayer
  code in `index.html`). The project ID currently checked in is a live Firebase project — lock
  down its Firestore security rules before relying on it, or swap in your own project's config.
