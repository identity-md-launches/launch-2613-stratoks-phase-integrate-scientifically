# Corrected learning and ecology evidence

These are local author measurements of the corrected source, not independent approval. Original raw evidence is unchanged in `tests/results/phase2a/`; final reruns are in `tests/results/correction/`. Both learning and ecology JSON files record hashes of the simulation modules. `node tests/experiments/report-correction.mjs` refuses stale hashes and altered seeds/resources.

## Controlled learning

Seeds 1–10, all four modes, all three original tasks, unchanged 300-trial acquisition / 400-trial reversal, 20% forced exposure, 10% reward noise and held-out hunger perturbation. This is a synthetic, two-target, one-action component task. It contains no emergency reflexes, navigation or competing action families. It tests conditional learned target preference; it cannot establish ecology fitness or the absence of action-count bias by itself.

| Task | Mode | Acquisition held-out, original → corrected | Reversal held-out, original → corrected | Corrected acquisition SD | Acquisition / reversal seeds <60% |
|---|---|---|---|---|---|
| location | legacy | 51.15% → 51.15% | 48.00% → 48.00% | 4.15% | 9 / 10 |
| location | mb-v1 | 98.60% → 98.60% | 98.30% → 98.30% | 2.06% | 0 / 0 |
| location | mb-v1-frozen | 49.55% → 49.55% | 50.50% → 50.50% | 5.40% | 10 / 10 |
| location | mb-v1-ablated | 49.55% → 49.55% | 50.50% → 50.50% | 5.40% | 10 / 10 |
| cue | legacy | 51.15% → 51.15% | 48.00% → 48.00% | 4.15% | 9 / 10 |
| cue | mb-v1 | 97.05% → 97.05% | 97.30% → 97.30% | 2.81% | 0 / 0 |
| cue | mb-v1-frozen | 49.55% → 49.55% | 50.50% → 50.50% | 5.40% | 10 / 10 |
| cue | mb-v1-ablated | 49.55% → 49.55% | 50.50% → 50.50% | 5.40% | 10 / 10 |
| threat | legacy | 51.15% → 51.15% | 48.00% → 48.00% | 4.15% | 9 / 10 |
| threat | mb-v1 | 96.90% → 96.90% | 96.70% → 96.70% | 2.50% | 0 / 0 |
| threat | mb-v1-frozen | 49.55% → 49.55% | 50.50% → 50.50% | 5.40% | 10 / 10 |
| threat | mb-v1-ablated | 49.55% → 49.55% | 50.50% → 50.50% | 5.40% | 10 / 10 |

All 120 serialized state and continuation comparisons agree. All held-out phases freeze weights. Frozen and ablated training now both produce zero neural updates. Earlier ablation scores already hid learned output, so its unchanged choice fraction concealed its plasticity defect; the new weight/counter regressions expose this. Run elapsed time: 7.31 seconds.

The hierarchy retains a single per-creature random draw and conditional softmax. With only one action in these experiments, target choice probabilities are the same as before. Unchanged learning fractions are expected, not evidence that the ecology regressions are absent. Legacy cannot distinguish the equal-feature targets. Frozen and ablated choices remain near chance. No failed seed was dropped.

## Autonomous ecology

The same ten initial worlds, 24 initial creatures, 5,000 ticks per mode/seed, unchanged `DEFAULTS.world`, no culling, refill, resource adjustment, forced training, reseeding or interventions. Values below are means across ten seeds. Raw JSON includes each seed, SD, range, hunger exposure, decision sources and neural/linear update counts.

| Mode | Population, original → corrected | Births | Deaths | Food | Complete shelters | Hungry creature-ticks (>70 hunger) |
|---|---|---|---|---|---|---|
| legacy | 42.50 → 42.50 | 18.70 → 18.70 | 0.20 → 0.20 | 247.38 → 247.38 | 12.20 → 12.20 | 3.84% → 3.84% |
| mb-v1 | 37.30 → 39.70 | 13.60 → 16.20 | 0.30 → 0.50 | 178.77 → 207.89 | 11.20 → 11.60 | 6.18% → 7.53% |
| mb-v1-frozen | 38.40 → 40.60 | 15.10 → 17.20 | 0.70 → 0.60 | 201.81 → 223.13 | 11.10 → 11.90 | 7.53% → 6.88% |
| mb-v1-ablated | 38.40 → 40.60 | 15.10 → 17.20 | 0.70 → 0.60 | 201.81 → 223.13 | 11.10 → 11.90 | 7.53% → 6.88% |

**Regression:** mb-v1 hunger exposure and mean deaths increase versus its original run even though population/births and food improve. Corrected mb-v1 still has lower population/births, fewer shelters, less food, more deaths and more hunger than legacy. Corrected frozen/ablated also exceed legacy hunger/deaths and have lower population. This is not an overall fitness improvement claim. Legacy per-seed rows match the original evidence exactly; ablated and frozen now have zero updates and identical behavior in their initially untrained worlds.

Ecology elapsed time: 75.36 seconds. SD in the experiment scripts uses division by n; these are descriptive samples, with no significance or generalization claim.

**Confounds and limits:** simultaneous fixes change emergency targets and action-family probabilities; these runs do not identify each fix’s separate contribution. Candidate availability, fixed priors, spatial binning, competition and shaped rewards remain engineered influences. Frozen/ablated worlds start untrained; trained-weight retention is tested separately. Seeds pair initial conditions, but changed choices diverge world RNG consumption through navigation/ecology, so later environments are not identical exposures. Five thousand ticks do not cover a full lifespan, extinction risk, long-term learning stability or storage growth. Survival reflexes are counted separately from model decisions; a later update after a reflex is an exposure, not evidence of learned selection.

## Capacity

**Real 512 MiB / 0.75 CPU Docker qualification is unverified:** Docker is unavailable on this worker. `tests/results/correction/docker/status.json` records the failed capability check. The runnable isolated runner is `node tests/load/correction-docker.mjs`; it enforces Docker memory/swap/CPU settings, checks `docker inspect` and in-container cgroup v2 values, and keeps service plus real clients inside that budget. No production data/volume/network is mounted.

The following completed fallback runs have **no requested resource enforcement**. They are diagnostic only; they do not establish supported VPS capacity. The service and clients share one process; all ecology stays enabled. Accelerated runs have 300 warm-up ticks plus 1,200 measured ticks; real-time runs have no warm-up and 180 ticks at a nominal one-second cadence. The runner’s process runtime includes initialization/warm-up/shutdown; measured runtime brackets only the measured ticks and a network drain.

| Mode | Initial → final creatures | Clients | Cadence | Measured runtime s | Process runtime s | Peak RSS MiB | Tick p95 / p99 ms | CPU ms/tick |
|---|---|---|---|---|---|---|---|---|
| legacy | 24 → 30 | 8 | accelerated | 2.99 | 3.89 | 133.17 | 1.505 / 17.545 | 2.562 |
| legacy | 100 → 100 | 8 | accelerated | 6.50 | 8.39 | 276.76 | 3.426 / 30.836 | 5.787 |
| legacy | 250 → 250 | 8 | accelerated | 17.35 | 21.48 | 357.22 | 8.251 / 72.353 | 16.780 |
| mb-v1 | 24 → 26 | 8 | accelerated | 2.87 | 3.78 | 137.33 | 1.636 / 20.123 | 2.541 |
| mb-v1 | 100 → 100 | 8 | accelerated | 7.66 | 9.73 | 288.59 | 3.631 / 57.437 | 6.680 |
| mb-v1 | 250 → 250 | 8 | accelerated | 19.58 | 24.45 | 421.79 | 8.369 / 142.152 | 17.169 |
| mb-v1-frozen | 24 → 26 | 8 | accelerated | 2.75 | 3.65 | 138.06 | 1.621 / 17.671 | 2.344 |
| mb-v1-frozen | 100 → 100 | 8 | accelerated | 7.62 | 9.78 | 281.69 | 3.657 / 53.648 | 6.744 |
| mb-v1-frozen | 250 → 250 | 8 | accelerated | 18.64 | 24.21 | 415.64 | 8.260 / 124.564 | 16.184 |
| mb-v1-ablated | 24 → 26 | 8 | accelerated | 2.80 | 3.65 | 134.36 | 1.523 / 18.242 | 2.449 |
| mb-v1-ablated | 100 → 100 | 8 | accelerated | 7.59 | 9.70 | 294.54 | 3.549 / 53.473 | 6.727 |
| mb-v1-ablated | 250 → 250 | 8 | accelerated | 18.28 | 23.09 | 419.88 | 8.228 / 124.292 | 15.774 |
| mb-v1 | 24 → 24 | 8 | 1 second | 179.12 | 179.36 | 97.31 | 8.739 / 16.339 | 7.087 |
| mb-v1 | 100 → 100 | 8 | 1 second | 179.17 | 179.50 | 144.05 | 13.682 / 51.064 | 12.166 |
| mb-v1 | 250 → 250 | 8 | 1 second | 179.22 | 179.80 | 216.90 | 20.113 / 133.666 | 37.490 |
| mb-v1 | 250 → 250 | 32 | accelerated | 48.71 | 62.55 | 433.16 | 18.973 / 145.154 | 50.819 |

Completed rows: 16 / 16. Platform, Node version, source hashes, tick durations/intervals, every client’s final tick, delta sizes, inspector payloads, population changes, process CPU/RSS and observed cgroup counters are retained with each row. Observed host cgroup counters do not demonstrate the requested limits. **Supported capacity on the 1 GB x86_64 VPS: not established.** Validate the real Docker matrix there before choosing a supported population/client ceiling. There is no automatic population cap.

