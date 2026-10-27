# Browser lab measurements

The exact `web/src/learningLab.ts` module was executed for seeds 1–10, three tasks and three modes: 30 cohorts / 90 policy runs. This is a synthetic controller experiment, not autonomous ecology or constrained-hardware benchmarking. The browser independently exercised the same compiled module; its downloaded JSON is retained in the browser evidence.

| Task | Mode | Acquisition held-out | Reversal held-out | Learned output removed | Acquisition below 60% |
|---|---|---|---|---|---|
| location | legacy | 50.35% ± 2.97 | 48.00% ± 2.05 | 50.00% ± 3.56 | 10/10 |
| location | mb-v1 | 98.15% ± 2.84 | 98.30% ± 2.25 | 49.95% ± 3.21 | 0/10 |
| location | mb-v1-frozen | 50.55% ± 3.38 | 50.50% ± 2.56 | 49.95% ± 3.21 | 10/10 |
| cue | legacy | 50.35% ± 2.97 | 48.00% ± 2.05 | 50.00% ± 3.56 | 10/10 |
| cue | mb-v1 | 97.10% ± 2.29 | 97.30% ± 1.90 | 49.95% ± 3.21 | 0/10 |
| cue | mb-v1-frozen | 50.55% ± 3.38 | 50.50% ± 2.56 | 49.95% ± 3.21 | 10/10 |
| threat | legacy | 50.35% ± 2.97 | 48.00% ± 2.05 | 50.00% ± 3.56 | 10/10 |
| threat | mb-v1 | 95.75% ± 6.79 | 96.70% ± 3.21 | 49.95% ± 3.21 | 0/10 |
| threat | mb-v1-frozen | 50.55% ± 3.38 | 50.50% ± 2.56 | 49.95% ± 3.21 | 10/10 |

Variability is population standard deviation across all ten seeds, not a standard error. No seeds or failed control runs are discarded. All low/high values and raw choices, rewards, forced indices and RNG endpoints are in [lab-results.json](lab-results.json). The lowest learning-enabled acquisition result is 76% in the punishment-only task; success in this controlled task is not evidence of superior survival in the full game.

Retention mismatches: **0 / 90**. Held-out phases with weight changes: **0**. The checkpoint comparison retains all mutable experiment inputs, weights and RNG, and compares 64 uninterrupted versus restored choices. The existing server tests separately exercise disk restart, backup and rollback; the browser checkpoint does not use or claim the server's full terrain serializer.

Protocol: evaluate 200 untrained trials, acquire 300, evaluate 200, check retention without advancing the experiment, reverse and train 400, evaluate 200, remove learned output and evaluate 200. Training has 20% forced exposure and 10% reward-sign noise. Held-out trials use hunger 0.45 rather than 0.4, new RNG draws, no forced exposure and no learning. They revisit the same sites; they do not test unseen-location transfer. Rewards are seeded/counterbalanced, never fixed to a site in the policy.

The food-cue task keeps locations within one coarse spatial bin and counterbalances the meaning of a visible fire cue. No emergency reflex is called. The danger task pairs one site with punishment and the other with zero reward. Legacy and frozen policies remain near chance; removing the learned output after training removes the preference. All three policies use the real server adapter and circuit implementation, imported directly. The UI contains no precomputed success values.

These rows differ slightly from historical backend results because this interactive protocol uses a 200-trial baseline and a non-advancing 64-choice checkpoint check. Historical `tests/results/phase2a/learning.json` uses its documented 100-trial baseline and continuation phase. Neither result set replaces the other.

Reproduce: `node web/scripts/measure-learning-lab.mjs`. Full-world ecology, 24/100/250-creature capacity, RSS and protocol measurements remain in [the unchanged backend report](../../docs/phase2a/RESULTS.md). That report is explicit about weaker ecological outcomes and outstanding exact Docker/cgroup validation.
