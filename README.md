# Stratoks · Phase 2A client integration

Observe the existing shared world, select a resident, and open **Learning → Brain / behavior**. The panel reads actual server decisions: active policy, sensed cues, candidate scores, learned associations, selection source and recent rewards. The terrain, characters, settlement layout, needs, memories, wallet authentication, history and intervention controls are preserved.

**Explore local demo** runs the same simulation engine privately in a browser worker, explicitly in `mb-v1` mode. **Try learning scenarios** opens a separate, synthetic experiment with legacy, learning-enabled and frozen policies. Neither experiment changes a connected server. No wallet is needed for either demo.

## Install, rebuild and preview

Node 24 was used for this release; use Node 22.12+ or 24 and npm. The server has no runtime npm dependencies. The frontend manifest, lockfile, Vite and TypeScript configuration are restored byte-for-byte from the verified recovered baseline.

```sh
node web/scripts/task.mjs install
node web/scripts/task.mjs typecheck
node web/scripts/task.mjs test
node web/scripts/licenses.mjs
node web/scripts/task.mjs build
node web/scripts/preview.mjs
```

Open `http://127.0.0.1:4173/preview/`. The build helper installs dependencies and caches under the operating system's temporary directory, outside this repository. It stages the source there, uses `npm ci` with the retained lockfile, and copies the finished export to **`dist/`**. Do not commit dependency directories. A fresh install needs the npm registry; the built site and server do not need a vendored registry or paid inference API.

`dist/index.html` and all relative runtime assets are supplied for static hosting at a subpath. No SPA rewrite is required. The client is ready for IMD's export pinning; **a public URL/CID is assigned after submission and is not yet available here**. Publication status is recorded in [publication.json](artifacts/phase2a-client/publication.json). No production deployment or live-world writes were performed.

## Two clients, one disposable server

```sh
node web/scripts/demo-server.mjs
```

Open the printed `http://127.0.0.1:4174/preview/` address in two tabs or browser profiles. This launcher starts the integrated client and a fresh, temporary `mb-v1` world at a one-second tick. It binds only loopback, ignores production configuration, and discards its temporary store on Ctrl-C. Its isolated configuration takes precedence over previously saved remote connection settings. It does not change the normal server default. The older companion demo remains available at `node server/bin/phase2a-demo.js` for historical component review.

For an owner-operated server, use **Settings → World service URL** with its HTTPS URL. An empty WebSocket field derives WSS `/ws`; a separate WSS URL can be configured explicitly. Settings persist in that browser. HTTP/WS is accepted only for loopback tests from a local page. The operator must allow the static client's exact origin through `ALLOWED_ORIGINS`. The shipped `web/public/world-config.json` and `dist/world-config.json` have empty URLs, with no guessed production endpoint or credentials.

The original wallet path remains signature-only: EIP-6963 browser wallets, mobile wallet deep links and Coinbase connector. The existing server cannot authenticate Coinbase passkey smart accounts; the client retains its explicit unsupported-signature message. There are no new tokens, contracts, payment or transaction flows.

## Learning lab

Choose food locations, food cues or learned danger and an integer seed from 1–100000. Reset applies that choice. Evaluate first for an untrained baseline, train 300 trials, evaluate without learning, reverse outcomes and train 400 trials, then evaluate again. Removing learned output retains trained weights but removes their score contribution. Check restore compares 64 uninterrupted choices with a JSON-restored experiment, including weights, creature inputs and both RNGs. This is not a server disk-backup test.

All three policies receive equal innate target scores, counterbalanced reward identity, 20% forced training exposure and 10% noisy reward signs. Evaluation uses 200 new draws, a different hunger input, no forced exposures and no updates. The cue task uses a visible fire marker with counterbalanced outcomes; the danger task uses location-linked punishment. No survival reflex is counted as learning. Scores, choices and failures are computed by the imported server controller, not precomputed UI values. Download the measured JSON to retain it; only 12 phases remain in memory and closing the panel discards the lab.

## Check the release

```sh
node --test --test-concurrency=2 tests/*.test.js
node web/scripts/task.mjs typecheck
node web/scripts/task.mjs test
node web/scripts/task.mjs build
node web/scripts/check-phase2a.mjs chromium
node web/scripts/check-phase2a.mjs webkit
node web/scripts/check-demo-launcher.mjs
node web/scripts/check-phase11.mjs artifacts/phase2a-client/auth-regression
node web/scripts/measure-learning-lab.mjs
node web/scripts/preflight-phase2a.mjs
```

Browser checks need Playwright's Chromium/WebKit installations and their system libraries. The locked development dependencies include Playwright and axe. Use the Playwright CLI inside the external directory printed by `node web/scripts/task.mjs path` to install browsers. The integration runner optionally accepts `CHROMIUM_EXECUTABLE_PATH` / `WEBKIT_EXECUTABLE_PATH` and uses a disposable server and two independent contexts. All screenshots are of the production export under `/preview/`. Fault-injected response checks are explicitly identified in the evidence.

Actual command results, fixed defects, browser coverage, design review and remaining limitations are in [the current validation report](artifacts/phase2a-client/VALIDATION.md). Prior `docs/results/`, `docs/recovery/` and `docs/phase2a/` reports retain their historical dates and scopes; they are not new test claims. Current code/export hashes and the added-path byte budget are in [release.json](artifacts/phase2a-client/release.json).

This release passed the production build and typecheck, 17 client tests, 68 server tests, 15 integration checks in each browser, 10 authenticated regression checks, 5 launcher checks and all 16 pinned design-probe checks. The six-domain review records unverified native-device, screen-reader, zoom and canvas-contrast coverage. `.gitignore` exposes only `artifacts/phase2a-client/` within the evidence tree, with an explicit 3 MiB path budget enforced by preflight; generated dependencies and caches remain excluded at every depth.

## Server, scientific scope and release limits

The complete server source, original tests and Docker package remain in `server/`, `tests/` and `deploy/`. No server interface or simulation file was changed by this client integration. Production defaults remain **`legacy`**. Operator activation, non-destructive schema migration, retained linear weights, deterministic circuit initialization and rollback on copied worlds are documented in [MIGRATION.md](docs/phase2a/MIGRATION.md). The versioned read-only JSON contract is [brain-v1.md](shared/brain-v1.md); this client tolerates old servers without that field.

- [Model comparison, primary citations, equations and code/data license distinctions](docs/phase2a/MODEL.md). This is an independently implemented, reduced mushroom-body-inspired circuit, not full-brain emulation, biological validation or consciousness. Wallets, construction, reproduction and relationships are game abstractions.
- [Ten-seed scientific experiments and capacity results](docs/phase2a/RESULTS.md), with raw data in `tests/results/phase2a/`. These earlier backend measurements remain applicable to unchanged backend code. They are not new Docker qualification. Exact Ubuntu 1 GB whole-host / 512 MB and 0.75 CPU cgroup verification, long-term capacity and ecological tradeoffs remain open.
- [Docker profile](deploy/phase2a-compose.yml) and [Dockerfile](deploy/Dockerfile) are retained. IMD serves the client, not this backend. Only the owner deploys after review.
- [Client/art attribution](docs/ASSETS.md), [static dependency notices](web/public/licenses/THIRD_PARTY_NOTICES.txt), and [locked dependency inventory](web/public/licenses/dependencies.json). No scientific dataset, connectome wiring or pretrained weights were added. The prior review flags the recovered backend's missing standalone redistribution grant; this integration does not resolve or invent that grant.
- [Author's release review](artifacts/phase2a-client/REVIEW.md). Test results and this review do not constitute independent approval. External scientific, authorization and operational review remains required before production activation.

Baseline: recovered commit `09af84d67722e30c0cb0c096ab8a8189a3b03166`; ZIP SHA-256 `8816bfda36545436f85d4ca0b13bd439be14fb3a6be285f25bd39f3edf8abd9e`. The named download and retained `deploy/recovered/stratoks-09af84d.zip` were reverified. The full original archive, including root documentation and the original build, is preserved. This delivery builds on accepted component commit `c6313b1c91e7ed12cb7fe8a9a4d866f8d2708ed2`; the network creates the final submission commit. Repository Git metadata was not changed.
