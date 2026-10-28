# STRATOKS · Phase 2A correction

The full shared-world application and **reduced mushroom-body-inspired circuit** are retained. This correction fixes emergency food selection, makes ablation a non-learning control, removes food-candidate count bias, and corrects the brain inspector. Production remains **legacy** until owner validation. No production data, VPS, contracts, art or payment integration was changed.

The reopened review fixes both reproduced findings on `ca7a177`: emergency selection now includes sensed food discarded by the memory cap, and retained decisions without captured mode metadata are labeled **Decision mode unrecorded**. [Revision evidence and issue-to-fix table](docs/correction/REVIEW.md).

Choose **Explore local demo**, select a resident, then **Learning**. The private worker runs the corrected engine. **Try learning scenarios** runs measured conditioning experiments without changing a connected server. The server URL remains owner-settable in Settings, with an empty shipped default. Wallet authentication and interventions remain in the full application; neither demo requires a wallet.

## Install, preview and rebuild

Use Node 22.12+ or 24 and npm. Application manifests, lockfile and build configuration are unchanged. The backend has zero runtime npm dependencies.

```sh
node web/scripts/task.mjs install
node web/scripts/task.mjs typecheck
node web/scripts/task.mjs test
node web/scripts/task.mjs build
node web/scripts/preview.mjs
```

Open `http://127.0.0.1:4173/preview/`. The helper uses `npm ci` against the retained lockfile, stages sources/dependencies under `/tmp`, and copies the production export to **dist/**. Relative asset URLs support static gateway subpaths. Source, lockfile, complete export, favicon, share image and license notices are delivered; no dependency/cache directories or registry archives are needed. To connect two clients to a disposable service, use `node web/scripts/demo-server.mjs` and open its printed URL in two profiles. Ctrl-C stops it; it never loads production data.

## Corrections and results

- Starvation chooses the nearest feasible site from all current observations plus retained memory before the ten-site cap, with numeric site-id ties, in every mode. Its source is **reflex**. Non-emergency targets retain learned selection and their existing cap.
- Frozen and ablated modes preserve existing circuit weights/counters; ablation also removes learned output. Policy learning is disabled in both. Wallet opinions retain the separate documented world `LEARNING` policy.
- New modes sample an action using its best target score, then a target conditionally. Extra EAT candidates cannot buy action probability. Legacy selection stays unchanged.
- **Learning history** distinguishes **Linear-policy updates** from circuit updates. Recent decisions span active policies; mean reward includes all completed rewarded actions. The inspector separates current plasticity from captured decision/outcome modes.

The final source passes **137 server tests (68 existing + 33 earlier + 36 review regressions)**, **17 client tests**, build/typecheck, **16 Chromium and 16 WebKit interaction checks**, **12 retained-history checks per engine**, and **16/16 pinned design-probe checks**. The original commit fails 22 of the 33 earlier regressions; `ca7a177` fails 16 of the 36 review regressions. See [final review](docs/correction/REVIEW.md), [raw commands](artifacts/phase2a-client/review/) and [design system](DESIGN.md).

The same 10 seeds were rerun for every learning task and all four ecology policies without resource changes. Controlled mb-v1 acquisition remains 96.90–98.60%; this synthetic task does not establish survival benefits. Versus `ca7a177`, mb-v1 averages 41.6 survivors instead of 39.7 and 2.86% hungry creature-ticks instead of 7.53%, but remaining food falls from 207.89 to 192.11. Food falls in all four modes. Legacy also changes because the required all-mode reflex fixes its starvation behavior; unmodified legacy ecology is no longer exactly equivalent. [Comparisons and confounds](docs/correction/RESULTS.md); original evidence stays under `tests/results/phase2a/`, previous-correction learning/ecology is preserved in `tests/results/review/`, final raw runs in `tests/results/correction/`.

## Reproduce checks

```sh
node --test --test-reporter=tap --test-concurrency=2 tests/*.test.js
node tests/experiments/reproduce-correction.mjs
node tests/experiments/reproduce-review.mjs --check-regressions
node web/scripts/check-review.mjs chromium
node web/scripts/check-review.mjs webkit
node tests/experiments/mushroom-learning.mjs 10 tests/results/correction/learning.json
node tests/experiments/mushroom-ecology.mjs 5000 10 tests/results/correction/ecology.json
node tests/experiments/report-correction.mjs
node web/scripts/check-phase2a.mjs chromium artifacts/phase2a-client/correction/chromium
node web/scripts/check-phase2a.mjs webkit artifacts/phase2a-client/correction/webkit
```

Browser checks use Playwright/axe installed by the helper. Install browsers with the Playwright CLI in the external directory printed by `node web/scripts/task.mjs path`; `PLAYWRIGHT_BROWSERS_PATH` can place them under `/tmp`. WebKit needs its Linux shared libraries; here these were extracted outside the repository. No browser or system packages are shipped. Runners manage their disposable preview/service and close them. Checks cover HTTP/WS agreement in two contexts, all policies, keyboard/focus, stale/error/retry states, lab training/reversal/ablation/download/restore, needs/memories/history and pause/resume. Native iPhone, screen-reader and native 200% zoom checks remain unperformed.

The assignment's pinned taste probe ran at 320, 390 and 1440 widths. Evidence is identified in the six-domain review. `node tests/experiments/check-correction.mjs` checks final source/export/evidence integrity and the 8 MiB contribution budget with read-only Git queries.

## VPS package and capacity

[VPS package and copy/migration steps](docs/correction/VPS.md), [review compose profile](deploy/correction-vps-compose.yml), [release manifest](docs/correction/RELEASE.json). `deploy/correction-vps.tar.gz` contains the corrected complete app/source/static client and server/test tools. Rebuild it with `python3 tests/experiments/package-correction.py`.

**Docker is unavailable here. Actual 512 MiB / 0.75 CPU qualification is unverified.** Run the isolated benchmark on a Docker/cgroup v2 x86_64 host:

```sh
node tests/load/correction-docker.mjs
```

It measures 24, 100 and 250 creatures with eight real clients across all modes, three one-second cadence runs, and a 250-creature/32-client run. It checks Docker/in-container limits and records raw RSS, CPU, tick p95/p99, throttling, memory events, population and client agreement. The local fallback is explicitly unenforced and does **not** establish supported capacity on a 1 GB VPS; `--local` is diagnostic only. Migration, restart, crash recovery and backup/restore pass on disposable stores. The 4,000-tick legacy differential test passes against the recovered engine with **only the specified starvation rule corrected** in its independent reference. This does not claim equivalence to the buggy unmodified reflex. No backend hosting is claimed.

## Static release and HTTPS

The exact offline-verified export CID is **bafybeifukwi4jdpv4sf572jkdung5zgkhe76nkchsxl2gmd5g62mpetqpm**. Import settings, hashes and source inventory are in [RELEASE.json](docs/correction/RELEASE.json). `deploy/correction-client.car.gz` reconstructs all 19 export files byte-for-byte. This is a computed address, **not a public pinning claim**; IMD may use different import settings when pinning dist/.

The previous ENS HTTPS URL reproduces the TLS failure. Tested CID gateways return HTTP 429; no working public gateway to this correction is certified. [Exact checks](docs/correction/HTTPS.json) identify the external publishing/DNS/TLS boundary. This worker has no IMD publishing tool or control of the gateway. After pinning, run:

```sh
node web/scripts/check-correction-https.mjs <actual-https-release-base-url-ending-in-slash>
```

It checks every file against the release bytes and rejects stale releases/challenge pages. [Publication handoff](docs/correction/PUBLICATION.md) includes CAR import and verification. The final submission commit is assigned by the network after this run; this revision starts at `ca7a1770779b3c55e519fc98ed80abe4b983fa7f`, following the original integration at `99e50b1c275b9422c14f279498b3e192b151992b`. An uncommitted content hash is not represented as that future commit.

[Scientific scope/citations](docs/phase2a/MODEL.md), [original migration/rollback](docs/phase2a/MIGRATION.md), [wallet/learning policy](server/docs/LEARNING.md), [attribution](docs/ASSETS.md) and all earlier evidence remain. This is a reduced circuit, not a complete fruit-fly brain or biological validation. Historical reports describe their original source; correction reports supersede their release/capacity claims for this code. The retained backend licensing boundary is unchanged.
