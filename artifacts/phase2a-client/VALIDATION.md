# Phase 2A integrated client validation

Date: 2026-10-27. **Complete for the stated client-integration scope.** The final production export is in `dist/`. IMD publication follows submission; a public URL is not available yet. This is the worker's evidence, not independent network certification or production approval.

The work restores the recovered React/Vite application and adds the real brain inspector, isolated browser experiments and a disposable two-client launcher. It preserves the original art and world layout. No accepted server, shared-interface, migration, model, Docker or existing test file was modified. The accepted backend science and capacity work is retained with its original limitations. There were no production connections, live-world writes or payment changes.

## Baseline and release identity

The named HTTPS ZIP was downloaded and its SHA-256 compared with the retained full archive: `8816bfda36545436f85d4ca0b13bd439be14fb3a6be285f25bd39f3edf8abd9e`. Both matched. Recovered commit: `09af84d67722e30c0cb0c096ab8a8189a3b03166`. `server/docs/LEARNING.md` and `docs/recovery/VALIDATION.md` were inspected before implementation. All 40 recovered `web/` files were imported before editing; [baseline-import.json](baseline-import.json) records their original/current checksums. Six restored files were extended. The original package manifest, lockfile, Vite/TypeScript configuration, renderer, icons, wallet and original tests remain byte-identical.

[release.json](release.json) pins the complete source and static-file hashes; [preflight.json](preflight.json) verifies the accepted inventory, complete archive, relative assets, empty public connection configuration and contribution size. Accepted parent: `c6313b1c91e7ed12cb7fe8a9a4d866f8d2708ed2`. The contributor network assigns the final commit; Git metadata was not modified.

Both final browser runs tested index SHA-256 `70c0709f3a3b25a25f92aa25fa024acb5395afee2234fff3947785f775060813`, and verified it did not change during the run. The index references content-hashed JS/CSS; the full export hashes are in the release inventory.

## Commands actually run

Node 24.21.0 / npm 11.19.0. Frontend dependencies were installed with the recovered lockfile in an external temporary build directory, with no repository `node_modules` or vendored registry. Browser installations and temporary WebKit support libraries were also outside the repository.

| Command | Actual result and evidence |
|---|---|
| `node web/scripts/task.mjs install` | Successful locked `npm ci`; original manifest and lockfile unchanged. |
| `node web/scripts/task.mjs typecheck` | Passed, no TypeScript diagnostics: [typecheck.txt](typecheck.txt). |
| `node web/scripts/task.mjs test` | **17/17 passed**, including ten-seed lab controls and deterministic replay: [client-tests.tap](client-tests.tap). |
| `node --test --test-concurrency=2 tests/*.test.js` | **68/68 passed** against the unchanged server, including persistence, backup/rollback, authentication, ecology and circuit tests: [server-tests.tap](server-tests.tap). |
| `node web/scripts/licenses.mjs` | Generated locked runtime dependency inventory and full notices, copied into the static export. |
| `node web/scripts/task.mjs build` | Successful Vite 8.3.5 production build: [build.txt](build.txt). |
| `node web/scripts/check-phase2a.mjs chromium` | **15/15 passed**, Chromium 156.0.8078.4: [checks](chromium/checks.json). |
| `node web/scripts/check-phase2a.mjs webkit` | **15/15 passed**, WebKit 27.2: [checks](webkit/checks.json). |
| `node web/scripts/check-demo-launcher.mjs` | **5/5 passed**: real CLI launcher, two tabs, one-second tick, isolated configuration precedence, displayed settings and static-write rejection: [result](demo-launcher.json). |
| `node web/scripts/check-phase11.mjs artifacts/phase2a-client/auth-regression` | **10/10 passed**: recovered authenticated interaction/history suite: [checks](auth-regression/client-checks.json). |
| `node web/scripts/measure-learning-lab.mjs` | 10 fixed seeds × 3 tasks × 3 policies; **0/90 retention mismatches**, no held-out weight changes: [raw results](lab-results.json). |
| Pinned `taste.mjs --out test/scratch/taste` | **16/16 checks passed** on the final export: [taste.json](taste.json). |
| `node web/scripts/preflight-phase2a.mjs` | Passed baseline, source/export integrity, metadata, dependency exclusions and explicit byte budgets: [result](preflight.json). |

The build warns that `node:worker_threads` (existing wallet dependency) and `node:fs` (shared config module) are externalized. The browser uses the latter's defaults/merge functions, not its Node file reader. Actual compiled private-world and learning workers ran successfully in both engines. These warnings remain recorded, not suppressed.

The pinned design probe was invoked from the repository root with `IMD_PLAYWRIGHT` pointing to the external locked Playwright module and `PLAYWRIGHT_BROWSERS_PATH` pointing to its external browser cache. Its script is a supplied assessment input and is removed by the network; the result is retained. WebKit initially lacked system libraries/EGL. A temporary external library tree and software-rendering launcher resolved that, after which the full checks passed. Earlier interrupted browser runs and the missing-library attempt are not counted as successful runs. WebKit here is Linux MiniBrowser, not a physical Safari device.

## Real integration and isolated learning

Each integration run starts a disposable real server, then connects two independent browser contexts at 390×844 and 1440×960. The server runs 900 actual world ticks before inspection. Both clients display its same creature, decision tick, selected action and candidate scores; the raw brain payload and SHA-256 are preserved in [shared-decision.json](chromium/shared-decision.json). Both then receive 24 further authoritative ticks over real WebSockets. The test controls tick progression to make these comparisons deterministic; the separate demo-launcher test verifies continuous one-second scheduling.

Tests exercise the welcome action by Tab/Enter, settings/Escape/focus return, Residents → Learning, reconnect with retained stale data, each lab task, acquisition, frozen evaluation, reversal, output ablation, checkpoint restore, JSON download, and the private world's Needs, Memories, History and pause/resume. Missing-brain and 429 responses are explicitly injected fixtures; normal shared decisions and all lab computations use the actual server/circuit code. No invented telemetry is displayed.

The lab/control checks compare the server's full world-state hash before and after the browser experiments and assert all intervening server requests are GETs. It remains unchanged. The isolated launcher also overrides a deliberately invalid saved remote endpoint and produces zero requests to it. The fixture is confined to a test, never shipped as configuration. Normal static `world-config.json` has empty URLs; HTTPS/WSS settings remain user-configurable. Production defaults remain `legacy`.

[LEARNING-RESULTS.md](LEARNING-RESULTS.md) reports every seed and all control failures. Mean acquisition held-out preference is 98.15% for food locations, 97.10% for cues and 95.75% for punishment-only avoidance; output removal returns the trained circuit to 49.95%. These are synthetic two-option tasks with equal innate scores and no emergency reflex, not improved survival claims. The legacy/frozen controls stay near chance. Reversal, variability and raw choices are retained. The browser checkpoint compares its complete mutable experiment state and 64 choices; server disk restart/backup/rollback are separate tests. Existing scientific and capacity reports are linked rather than replaced.

## Better Interface coverage

The pinned workflow and all six domain cores were read and applied during implementation. The review targets the changed inspector/lab, affected settings and entry states, and the retained world shell. The original visual direction takes precedence over unrelated redesign preferences. [DESIGN.md](../../DESIGN.md) records actual final tokens, font scale, components, spacing and responsive rules.

| Domain | Coverage and evidence | Limits / not applicable |
|---|---|---|
| Accessibility — Checked | Native buttons, selects, disclosures, table headers/caption, explicit form labels, status/error text and focus styles checked in source. Tab/Enter reaches the main action; Escape closes Settings and restores focus. Focused primary screenshot inspected. Axe scans of entry, real brain view and lab results found **0 violations in each state in each engine**. Reduced-motion state exercised. | No screen-reader session, physical-device test or native 200% browser-zoom test. Not every focus stop/background was manually inspected. Taste reports 8 retained controls below the comfortable 44px target; all 14 meet its 24px-or-spacing criterion. |
| Layout — Checked | Entry at 320/390/1440; inspector/lab at 320/390/800/1440; 667×375 landscape. No page/panel horizontal overflow. Final mobile and desktop screenshots inspected. Existing side-panel flow retained; mode/selection comes before disclosures. | Long panels intentionally scroll vertically. Every possible viewport/content combination is not tested. No separate route or new dashboard is needed. |
| Writing — Checked | Explicit local/server distinctions, action-oriented labels, mode and decision-source labels, bounded history, training/evaluation separation, retry guidance and no consciousness/full-brain claims. Entry has product/main action above fold, a five-word headline and 21 prose words at 390. | Existing art speech remains labeled template. Only English is supported; translation/RTL review is not applicable to this assignment. |
| Typography — Checked | Existing Manrope, six-size token scale and 400/600/800 weights retained. Fixed table columns, wrapping identifiers, signed values and tabular digits checked. Taste sees four sizes at 390 and six including one-offs at desktop. | Text enlargement independently of viewport size was not tested. |
| Colors — Checked | Existing semantic tokens reused. Numbers/text convey selection, reward sign, policy and learning state independently of color. Taste's measured solid text pairs meet 4.5:1 (3:1 large); axe scans add rendered checks. | Taste cannot measure 45 text boxes over canvas/images/gradients. Those pairs are **not verified**, not claimed compliant. No dark theme was added. |
| UI — Checked | Original canvas/art/icons and panel shell preserved. New disclosures and result meters reuse components; loading, empty, busy, stale, missing-interface and retry states exercised. Worker state is bounded and terminates on close. No extra animation, decorative cards, payment flow or new wallet infrastructure. | Native OS wallet/passkey UI and real wallet signatures were not exercised; the recovered automated auth suite uses test-generated accounts. |

Screenshots inspected: [entry at 390](chromium/first-screen-390.jpg), [keyboard focus](chromium/keyboard-primary-390.jpg), [brain at 390](chromium/brain-390.jpg), [brain at 1440 in WebKit](webkit/brain-1440.jpg), [lab at 390](chromium/lab-390.jpg), [reversal results](webkit/reversal-390.jpg), [landscape](chromium/lab-landscape-667.jpg). The original landscape and the main local-world action are visible on the first 390px screen. Metadata includes title, favicon, description, `og:title` and local `og:image`. The actual export runs at `/preview/` with relative runtime assets, no missing static resources or uncaught application exceptions in completed integration runs.

## Findings, fixes and rechecks

Locations refer to the final source. Each root cause is recorded once.

| Severity / source | Observed issue and impact | Fix and recheck |
|---|---|---|
| High · `web/src/BrainBehavior.tsx:20` | Recovered client showed legacy learning summaries without the accepted brain-interface data, so users could not inspect the new policy. | Real detail payload now drives mode, source, selection, normalized cues, candidate associations and rewards; two-client payload/DOM agreement passed in both engines. |
| High · `web/src/learningLab.ts:31` | An initial browser restore implementation called the Node terrain serializer, causing `Buffer is not defined`. | Serialize only the complete experiment checkpoint with browser-safe JSON; actual compiled-worker restore/download checks passed, plus 90 deterministic retention checks. The narrower scope is explicitly labeled. |
| Medium · `web/src/LearningLab.tsx:52` | Implicit scenario labeling included option text in the accessible name, undermining the intended exact label. | Explicit `htmlFor`/`id` bindings for scenario and seed; exact-name browser interactions and axe checks passed. |
| Medium · `web/src/Panels.tsx:207` | Switching connected/reconnecting state reset the inspector tab and discarded visible details. | Reset on creature/source/world/epoch changes, preserve view during transport recovery, show stale status. Offline/reconnect and 429 recovery passed in both engines. |
| High · `web/src/App.tsx:92` | A prior saved remote URL could supersede the disposable launcher's connection configuration. | Only an explicit loopback isolated config overrides saved settings. A fixture with saved remote settings produced zero remote requests, two tabs shared the local world, and Settings displayed the actual local URL. |
| Medium · `web/src/BrainBehavior.tsx:26` and `web/src/styles.css:42` | Early panel ordering put useful selection information below extensive cue telemetry. | Lead with mode and selected action; disclose sensed/circuit detail. Final 390 screenshot shows the decision without changing the world layout; no overflow across tested widths. |
| High · `.gitignore:1` | Repository-local Git exclusions hide all `artifacts/`, which would omit the requested measured evidence. | Added a precise exception for `artifacts/phase2a-client/` with a **3,145,728-byte** path budget, enforced by preflight. Generated dependency/cache directories stay excluded at every depth. |

Harness-only corrections: use the actual composed text for the 429 locator; close the mobile side panel before reaching pause (the existing layout intentionally hides it while a panel is open); explicitly label any response fixtures. These are not application fixes or evidence of a layout regression.

## Packaging and unresolved external gates

The explicit evidence path budget is 3 MiB. The complete added contribution (`web/`, `dist/`, evidence, README, DESIGN and the new ignore file) is measured uncompressed against 8,388,608 bytes with a further 196,608-byte reserve. The exact result is in preflight. Existing accepted archives and evidence are preserved, not silently dropped. No dependency/cache archives, symlinks/submodules or node_modules are added. Root ignore rules only expose this bounded evidence path and exclude generated directories.

The complete static export includes original art/share assets, font, workers and dependency notices. Build warnings and failed development attempts are disclosed above. No Docker build or exact target-host benchmark was performed in this client integration. Earlier 24/100/250-creature RSS/tick/payload measurements remain in `docs/phase2a/RESULTS.md`, including their limitations; they do not establish the exact requested Ubuntu/1 GB/512 MB/0.75 CPU deployment profile or long-duration sustainability.

Before production activation the owner still needs independent scientific/authorization/regression review, exact target-host capacity qualification, resolution of the recovered backend's standalone redistribution grant, and an owner-operated HTTPS/WSS service. No restricted connectome data was introduced. Biological validity and some weaker ecological outcomes remain explicit scientific limitations. IMD's URL and final source commit are assigned after submission. [REVIEW.md](REVIEW.md) is an author's review of this exact release, not external sign-off.
