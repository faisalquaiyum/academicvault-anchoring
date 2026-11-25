# AcademicVault results (auto-generated)
_Generated 2026-11-25T07:39:36.553913+00:00 | folds: monthly (20) | gas: PLACEHOLDER (not measured) | data: real_

## Claims check
| claim | status | evidence |
|---|---|---|
| Batching cuts modelled cost by >= 90 % versus anchoring every certificate immediately | SUPPORTED | reduction 97.11-98.08 % across policies (main config); CONDITIONAL on placeholder gas |
| The ML window classifier beats the hour-of-day prior (regret, pooled walk-forward) | NOT SUPPORTED (CI includes 0) | diff -2.11 pts [-7.79, +3.32]; beats hour prior in 12/20 folds |
| ML-driven window policy (P5) is cheaper than the hour-prior policy (P4) | NOT SUPPORTED (CI includes 0) | cost diff -1.04 % [-3.4, +2.3] over 20 folds |
| A perfect window label (P6) makes the window policy cheaper than the hour prior (P4) | OPPOSITE (A costlier, CI above 0) | cost diff +4.75 % [+0.7, +8.7] over 20 folds |
| ML-driven window policy (P5) is cheaper than the plain fee threshold (P2) | OPPOSITE (A costlier, CI above 0) | cost diff +11.70 % [+2.2, +23.6] over 20 folds |
| Timing headroom is small: even a clairvoyant reference adds <= 0.5 percentage points of reduction over the best realistic policy | SUPPORTED | P8 minus best realistic policy = +0.29 pp (main config) |
| The RL agent makes its own anchor decisions (not only guard/full-queue anchors) | SUPPORTED | 25.7 % of RL anchors were policy-initiated |
| RL results are stable across independent training seeds (relative sd <= 5 %) | NOT SUPPORTED | max relative sd over seeds = 28.7 % |
| RL is cheaper than the best tuned rule at the same average-wait budget (validation-selected, fold-paired CI below 0) | NOT SUPPORTED | RL clearly cheaper in 0/6 (workload, budget) cells; clearly costlier in 6; indistinguishable in 0 |
| RL matches (is not worse than) the best tuned rule at the same budget | NOT SUPPORTED | RL clearly costlier in 6/6 cells |
| Every simulated run meets the 24 h SLA | SUPPORTED | min SLA compliance = 100.0 %; 4,440 invariant checks |
| Batching cuts modelled cost by >= 90 % at every SLA tested (main configuration) | SUPPORTED | min reduction by SLA: 6 h: 96.96 %, 12 h: 97.10 %, 24 h: 97.11 %, 48 h: 97.10 % |
| Clairvoyant headroom stays <= 0.5 percentage points at every SLA tested | SUPPORTED | P8 gap by SLA: 6 h: +0.44 pp, 12 h: +0.35 pp, 24 h: +0.29 pp, 48 h: +0.29 pp |
| Slack-awareness alone (P9) is cheaper than a tuned static percentile rule (P2p) at equal wait | MIXED | clearly cheaper in 1/6 (workload, wait) cells; clearly costlier in 1; indistinguishable in 4 |
| The slack-ramp rule (P9) is cheaper than the best static rule at equal wait | NOT SUPPORTED | clearly cheaper in 0/6 (workload, wait) cells; clearly costlier in 1; indistinguishable in 5 |
| The ML wait-value trigger (P10) is cheaper than the same trigger with an hour-of-day prior (P10p) at equal wait | MIXED | clearly cheaper in 5/6 (workload, wait) cells; clearly costlier in 0; indistinguishable in 1 |
| ML adds value on top of slack-awareness (P10 cheaper than P9) at equal wait | MIXED | clearly cheaper in 1/6 (workload, wait) cells; clearly costlier in 0; indistinguishable in 5 |
| The ML wait-value trigger (P10) is cheaper than the best static rule at equal wait | NOT SUPPORTED | clearly cheaper in 0/6 (workload, wait) cells; clearly costlier in 0; indistinguishable in 6 |
| The ML wait-value trigger (P10) is cheaper than tabular RL (P7) at equal wait | MIXED | clearly cheaper in 5/6 (workload, wait) cells; clearly costlier in 0; indistinguishable in 1 |
| Even the true value of waiting (P10o, ceiling) makes the trigger clearly cheaper than the best static rule at equal wait | MIXED | clearly cheaper in 1/6 (workload, wait) cells; clearly costlier in 0; indistinguishable in 5 |
| The ML forecast of the value of waiting is closer to the truth than the hour-of-day prior (MAE, test folds) | SUPPORTED | ML better in a majority of folds at 5/5 horizons; skill vs prior: 1 h: +17.8%, 3 h: +29.6%, 6 h: +37.5%, 12 h: +42.8%, 24 h: +43.1% |

## Readiness
| item | status | how to fix |
|---|---|---|
| Real fee data (not the synthetic fallback) | OK |  |
| Gas model measured, not placeholder | TODO | create measured_gas.csv (testnet / Hardhat gas report); absolute savings depend on it |
| Fee-data source documented | TODO | fill DATA_SOURCE_NOTE in the config cell |
| Real issuance trace used | TODO | add issuance_times.csv; until then workloads are synthetic |
| >= 3 independent RL seeds per setting | OK |  |
| >= 12 walk-forward folds (more statistical power) | OK |  |
| All scheduler invariants passed | OK |  |
| SLA sensitivity run (6/12/24/48 h) | OK |  |
| [v11] Slack-aware timing section run (7i) | OK |  |

## anchor_triggers_main
| policy | guard | full | policy_rule | policy-initiated % |
|---|---|---|---|---|
| P1 Fixed 12 h | 0 | 10096 | 60 | 0.6 |
| P2 Threshold (no ML) | 44 | 5227 | 8496 | 61.7 |
| P2b Fee-dep. queue threshold | 52 | 2902 | 13235 | 81.8 |
| P3 Window random | 4 | 7794 | 6644 | 46 |
| P4 Window hour prior | 0 | 7625 | 6202 | 44.9 |
| P5 Window ML | 0 | 7626 | 6165 | 44.7 |
| P6 Window oracle label | 1 | 7219 | 7243 | 50.1 |
| P7 RL (Q-learning) | 21 | 8652 | 2996 | 25.7 |
| P8 Clairvoyant (future-fee) | 39 | 7189 | 4363 | 37.6 |

## candidates_all
_2,520 rows: see candidates_all.csv_

## cost_vs_wait_points
| rate | cap | policy | cost_eth | avg_wait_min |
|---|---|---|---|---|
| 0.05 | 50 | P1 Fixed 12 h | 0.007264 | 401.7 |
| 0.05 | 50 | P2 Threshold (no ML) | 0.006183 | 290.8 |
| 0.05 | 50 | P2b Fee-dep. queue threshold | 0.006184 | 290.8 |
| 0.05 | 50 | P3 Window random | 0.005573 | 496.5 |
| 0.05 | 50 | P4 Window hour prior | 0.003321 | 539.6 |
| 0.05 | 50 | P5 Window ML | 0.003492 | 547 |
| 0.05 | 50 | P6 Window oracle label | 0.003852 | 481.8 |
| 0.05 | 50 | P8 Clairvoyant (future-fee) | 0.004821 | 350.7 |
| 0.2 | 50 | P1 Fixed 12 h | 0.008533 | 372.6 |
| 0.2 | 50 | P2 Threshold (no ML) | 0.00746 | 290.4 |
| 0.2 | 50 | P2b Fee-dep. queue threshold | 0.00861 | 236.1 |
| 0.2 | 50 | P3 Window random | 0.008115 | 432.4 |
| 0.2 | 50 | P4 Window hour prior | 0.005025 | 452.1 |
| 0.2 | 50 | P5 Window ML | 0.005993 | 448.2 |
| 0.2 | 50 | P6 Window oracle label | 0.005247 | 420.7 |
| 0.2 | 50 | P7 RL (Q-learning) | 0.006183 | 468.3 |
| 0.2 | 50 | P8 Clairvoyant (future-fee) | 0.004919 | 355.6 |
| 1 | 50 | P1 Fixed 12 h | 0.02253 | 124.3 |
| 1 | 50 | P2 Threshold (no ML) | 0.02508 | 98.68 |
| 1 | 50 | P2b Fee-dep. queue threshold | 0.0274 | 83.54 |
| 1 | 50 | P3 Window random | 0.0306 | 112 |
| 1 | 50 | P4 Window hour prior | 0.02784 | 110.4 |
| 1 | 50 | P5 Window ML | 0.02804 | 110 |
| 1 | 50 | P6 Window oracle label | 0.02837 | 108.3 |
| 1 | 50 | P7 RL (Q-learning) | 0.02292 | 117.1 |
| 1 | 50 | P8 Clairvoyant (future-fee) | 0.02053 | 112.5 |

## frontier_all
| workload | family | setting | cost_eth | cost_sd_over_rl_seeds | wait_min | wait_sd_over_rl_seeds | transactions |
|---|---|---|---|---|---|---|---|
| bursty 0.2/step + bursts | P1 fixed interval | 1 h | 0.06873 | nan | 28.77 | nan | 505.2 |
| bursty 0.2/step + bursts | P1 fixed interval | 12 h | 0.01186 | nan | 233.3 | nan | 80.25 |
| bursty 0.2/step + bursts | P1 fixed interval | 2 h | 0.04228 | nan | 48.8 | nan | 307.9 |
| bursty 0.2/step + bursts | P1 fixed interval | 3 h | 0.03161 | nan | 67.94 | nan | 224.8 |
| bursty 0.2/step + bursts | P1 fixed interval | 4 h | 0.02582 | nan | 86.92 | nan | 179.9 |
| bursty 0.2/step + bursts | P1 fixed interval | 5 h | 0.0218 | nan | 106.3 | nan | 151 |
| bursty 0.2/step + bursts | P1 fixed interval | 6 h | 0.01846 | nan | 125.1 | nan | 131.4 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=1 | 0.03512 | nan | 141.8 | nan | 598.7 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=10 | 0.01131 | nan | 192.5 | nan | 134.6 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=15 | 0.01022 | nan | 218.8 | nan | 105.6 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=20 | 0.009508 | nan | 244 | nan | 89.85 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=25 | 0.009819 | nan | 267.7 | nan | 79.92 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=30 | 0.009505 | nan | 291.9 | nan | 73 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=35 | 0.009799 | nan | 314.4 | nan | 67.8 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=40 | 0.00893 | nan | 331.5 | nan | 64.23 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=45 | 0.009398 | nan | 350.8 | nan | 61.58 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=5 | 0.01503 | nan | 163.6 | nan | 209.8 |
| bursty 0.2/step + bursts | P2 threshold | min_batch=50 | 0.009019 | nan | 365.2 | nan | 59.95 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=1 | 0.03649 | nan | 110.9 | nan | 617.5 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=10 | 0.01238 | nan | 158.1 | nan | 147.7 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=15 | 0.01103 | nan | 183.3 | nan | 117.4 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=20 | 0.01044 | nan | 204.5 | nan | 101.5 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=25 | 0.009935 | nan | 220 | nan | 92.98 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=30 | 0.009716 | nan | 252.4 | nan | 81.53 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=35 | 0.009058 | nan | 285.3 | nan | 72.85 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=40 | 0.009511 | nan | 316.7 | nan | 66.85 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=45 | 0.009119 | nan | 343.2 | nan | 62.65 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=5 | 0.01619 | nan | 131.4 | nan | 225.9 |
| bursty 0.2/step + bursts | P2b fee-dep. queue | min_batch=50 | 0.009019 | nan | 365.2 | nan | 59.95 |
| bursty 0.2/step + bursts | P7 RL | delay=0.0005 | 0.01191 | 0.0007191 | 304.1 | 11.72 | 99.01 |
| bursty 0.2/step + bursts | P7 RL | delay=0.002 | 0.01181 | 0.0002173 | 279.9 | 10.19 | 105.7 |
| bursty 0.2/step + bursts | P7 RL | delay=0.005 | 0.01768 | 0.001622 | 189.9 | 12.21 | 163.6 |
| bursty 0.2/step + bursts | P7 RL | delay=0.02 | 0.03058 | 0.006988 | 140.3 | 13.91 | 223.7 |
| bursty 0.2/step + bursts | P7 RL | delay=0.05 | 0.02571 | 0.007372 | 166.7 | 33.68 | 205.8 |
| poisson 1.0/step | P1 fixed interval | 1 h | 0.08817 | nan | 29.64 | nan | 654.5 |
| poisson 1.0/step | P1 fixed interval | 12 h | 0.02253 | nan | 124.3 | nan | 169.3 |
| poisson 1.0/step | P1 fixed interval | 2 h | 0.04656 | nan | 59.73 | nan | 340.2 |
| poisson 1.0/step | P1 fixed interval | 3 h | 0.02999 | nan | 90.2 | nan | 230 |
| poisson 1.0/step | P1 fixed interval | 4 h | 0.02564 | nan | 114.2 | nan | 181.7 |
| poisson 1.0/step | P1 fixed interval | 5 h | 0.02314 | nan | 122.6 | nan | 169.9 |
| poisson 1.0/step | P1 fixed interval | 6 h | 0.02253 | nan | 123.2 | nan | 169.3 |
| poisson 1.0/step | P2 threshold | min_batch=1 | 0.09611 | nan | 70.78 | nan | 1564 |
| poisson 1.0/step | P2 threshold | min_batch=10 | 0.03367 | nan | 80.79 | nan | 391.3 |
| poisson 1.0/step | P2 threshold | min_batch=15 | 0.02855 | nan | 87.09 | nan | 305.8 |
| poisson 1.0/step | P2 threshold | min_batch=20 | 0.02658 | nan | 92.73 | nan | 259.6 |
| poisson 1.0/step | P2 threshold | min_batch=25 | 0.02508 | nan | 98.68 | nan | 229.4 |
| poisson 1.0/step | P2 threshold | min_batch=30 | 0.02433 | nan | 105 | nan | 209.2 |
| poisson 1.0/step | P2 threshold | min_batch=35 | 0.02392 | nan | 110.7 | nan | 194.3 |
| poisson 1.0/step | P2 threshold | min_batch=40 | 0.02223 | nan | 115.9 | nan | 182.8 |
| poisson 1.0/step | P2 threshold | min_batch=45 | 0.02386 | nan | 121.9 | nan | 174.5 |
| poisson 1.0/step | P2 threshold | min_batch=5 | 0.04478 | nan | 74.91 | nan | 609.2 |
| poisson 1.0/step | P2 threshold | min_batch=50 | 0.02256 | nan | 126.5 | nan | 169.3 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=1 | 0.0992 | nan | 58.68 | nan | 1605 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=10 | 0.03692 | nan | 67.87 | nan | 427.8 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=15 | 0.03246 | nan | 73.74 | nan | 341.5 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=20 | 0.02905 | nan | 78.71 | nan | 295.8 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=25 | 0.0274 | nan | 83.54 | nan | 269.8 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=30 | 0.02506 | nan | 92.52 | nan | 236.3 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=35 | 0.02576 | nan | 101 | nan | 211.5 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=40 | 0.02476 | nan | 109.2 | nan | 193.1 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=45 | 0.02303 | nan | 118 | nan | 178.9 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=5 | 0.04773 | nan | 62.52 | nan | 647.1 |
| poisson 1.0/step | P2b fee-dep. queue | min_batch=50 | 0.02256 | nan | 126.5 | nan | 169.3 |
| poisson 1.0/step | P7 RL | delay=0.0005 | 0.02275 | 0.0001174 | 123.3 | 1.328 | 179.5 |
| poisson 1.0/step | P7 RL | delay=0.002 | 0.02291 | 0.0001999 | 121.7 | 1.682 | 179.7 |
| poisson 1.0/step | P7 RL | delay=0.005 | 0.02306 | 0.0002717 | 120.5 | 3.76 | 184.1 |
| poisson 1.0/step | P7 RL | delay=0.02 | 0.02347 | 0.0008717 | 119.7 | 2.03 | 192.2 |
| poisson 1.0/step | P7 RL | delay=0.05 | 0.02804 | 0.005085 | 112.8 | 3.369 | 326.4 |

## gas_sensitivity
| policy | 0 | 2000 | 5000 |
|---|---|---|---|
| P1 Fixed 12 h | 97.79 | 95.58 | 92.26 |
| P2 Threshold (no ML) | 97.63 | 95.56 | 92.44 |
| P2b Fee-dep. queue threshold | 97.41 | 95.38 | 92.34 |
| P4 Window hour prior | 97.38 | 95.17 | 91.86 |
| P5 Window ML | 97.44 | 95.23 | 91.93 |
| P7 RL (Q-learning) | 97.67 | 95.52 | 92.3 |
| P8 Clairvoyant (future-fee) | 98.08 | 96.28 | 93.58 |

## matched_budget_by_fold
_480 rows: see matched_budget_by_fold.csv_

## matched_budget_rl_vs_rules
| workload | budget_min | RL vs | cost diff % (RL vs rule) | 95% CI (folds) | RL cheaper in folds | wait diff (min) |
|---|---|---|---|---|---|---|
| poisson 1.0/step | 80 | P1 fixed interval | 7.95 | [-18.4, +41.9] | 10/20 | 19.6 |
| poisson 1.0/step | 80 | P2 threshold | 35.87 | [+4.6, +72.3] | 7/20 | 1.8 |
| poisson 1.0/step | 80 | P2b fee-dep. queue | 76.64 | [+36.6, +126.1] | 3/20 | 0.4 |
| poisson 1.0/step | 80 | best rule on average (P2b fee-dep. queue) | 76.64 | [+36.6, +126.1] | 3/20 | 0.4 |
| poisson 1.0/step | 100 | P1 fixed interval | 16.57 | [-8.0, +48.0] | 13/20 | -0.4 |
| poisson 1.0/step | 100 | P2 threshold | 42.64 | [+13.3, +80.3] | 5/20 | -6.8 |
| poisson 1.0/step | 100 | P2b fee-dep. queue | 41.31 | [+11.2, +81.0] | 5/20 | -5.8 |
| poisson 1.0/step | 100 | best rule on average (P2 threshold) | 42.64 | [+13.3, +80.3] | 5/20 | -6.8 |
| poisson 1.0/step | 120 | P1 fixed interval | 32.31 | [+2.3, +71.0] | 7/20 | -20.9 |
| poisson 1.0/step | 120 | P2 threshold | 52.59 | [+19.8, +92.6] | 2/20 | -22.9 |
| poisson 1.0/step | 120 | P2b fee-dep. queue | 43.31 | [+12.0, +82.7] | 4/20 | -21.9 |
| poisson 1.0/step | 120 | best rule on average (P2 threshold) | 52.59 | [+19.8, +92.6] | 2/20 | -22.9 |
| bursty 0.2/step + bursts | 150 | P1 fixed interval | -11.81 | [-23.6, -0.3] | 15/20 | 15.3 |
| bursty 0.2/step + bursts | 150 | P2 threshold | -6.55 | [-24.7, +14.0] | 13/20 | -21.5 |
| bursty 0.2/step + bursts | 150 | P2b fee-dep. queue | 30.01 | [+9.9, +50.9] | 4/20 | -15.5 |
| bursty 0.2/step + bursts | 150 | best rule on average (P2b fee-dep. queue) | 30.01 | [+9.9, +50.9] | 4/20 | -15.5 |
| bursty 0.2/step + bursts | 200 | P1 fixed interval | -13.63 | [-28.9, +4.5] | 15/20 | 45.4 |
| bursty 0.2/step + bursts | 200 | P2 threshold | 28.48 | [+13.1, +45.3] | 5/20 | -10.2 |
| bursty 0.2/step + bursts | 200 | P2b fee-dep. queue | 45.7 | [+30.2, +63.0] | 1/20 | -3.1 |
| bursty 0.2/step + bursts | 200 | best rule on average (P2b fee-dep. queue) | 45.7 | [+30.2, +63.0] | 1/20 | -3.1 |
| bursty 0.2/step + bursts | 250 | P1 fixed interval | -14.22 | [-25.7, -4.4] | 15/20 | 36.4 |
| bursty 0.2/step + bursts | 250 | P2 threshold | 10.21 | [+0.3, +20.6] | 7/20 | 13.6 |
| bursty 0.2/step + bursts | 250 | P2b fee-dep. queue | 16.16 | [+4.3, +28.1] | 6/20 | 3.8 |
| bursty 0.2/step + bursts | 250 | best rule on average (P2b fee-dep. queue) | 16.16 | [+4.3, +28.1] | 6/20 | 3.8 |

## matched_budget_summary
| workload | budget_min | family | test_cost_eth | test_wait_min | folds_feasible_on_val | folds |
|---|---|---|---|---|---|---|
| poisson 1.0/step | 80 | P1 fixed interval | 0.04656 | 59.73 | 20 | 20 |
| poisson 1.0/step | 80 | P2 threshold | 0.0437 | 77.62 | 20 | 20 |
| poisson 1.0/step | 80 | P2b fee-dep. queue | 0.03025 | 78.99 | 20 | 20 |
| poisson 1.0/step | 80 | P7 RL | 0.0475 | 79.38 | 12 | 20 |
| poisson 1.0/step | 100 | P1 fixed interval | 0.02999 | 90.2 | 20 | 20 |
| poisson 1.0/step | 100 | P2 threshold | 0.02501 | 96.66 | 20 | 20 |
| poisson 1.0/step | 100 | P2b fee-dep. queue | 0.026 | 95.62 | 20 | 20 |
| poisson 1.0/step | 100 | P7 RL | 0.03794 | 89.82 | 18 | 20 |
| poisson 1.0/step | 120 | P1 fixed interval | 0.02626 | 111.8 | 20 | 20 |
| poisson 1.0/step | 120 | P2 threshold | 0.02305 | 113.8 | 20 | 20 |
| poisson 1.0/step | 120 | P2b fee-dep. queue | 0.0233 | 112.8 | 20 | 20 |
| poisson 1.0/step | 120 | P7 RL | 0.03763 | 90.95 | 19 | 20 |
| bursty 0.2/step + bursts | 150 | P1 fixed interval | 0.01867 | 122.4 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P2 threshold | 0.03024 | 159.2 | 13 | 20 |
| bursty 0.2/step + bursts | 150 | P2b fee-dep. queue | 0.01774 | 153.2 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P7 RL | 0.01849 | 137.7 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P1 fixed interval | 0.01785 | 150.2 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P2 threshold | 0.01375 | 205.8 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P2b fee-dep. queue | 0.01115 | 198.7 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P7 RL | 0.01628 | 195.6 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P1 fixed interval | 0.01255 | 215.4 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P2 threshold | 0.009785 | 238.2 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P2b fee-dep. queue | 0.009706 | 248.1 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P7 RL | 0.01076 | 251.9 | 20 | 20 |

## paired_cost_wait_ci
| A | B | folds | cost diff % (A vs B) | cost 95% CI | A cheaper in folds | wait diff (min) | wait 95% CI |
|---|---|---|---|---|---|---|---|
| P5 | P4 | 20 | -1.04 | [-3.4, +2.3] | 14 | -0.3 | [-0.8, +0.1] |
| P5 | P2 | 20 | 11.7 | [+2.2, +23.4] | 5 | 11.3 | [+10.1, +12.8] |
| P7 | P1 | 20 | 6.85 | [+1.0, +16.5] | 3 | -7.3 | [-15.7, -0.4] |
| P2 | P1 | 20 | 9.23 | [+5.4, +13.6] | 3 | -25.7 | [-27.2, -24.3] |
| P8 | P2 | 20 | -17.46 | [-21.0, -14.1] | 20 | 13.8 | [+12.1, +15.7] |
| P8 | P4 | 20 | -23.9 | [-28.9, -19.9] | 20 | 2.1 | [+1.4, +2.9] |
| P6 | P4 | 20 | 4.75 | [+0.8, +8.7] | 5 | -2.1 | [-2.8, -1.4] |

## policy_summary_main
| policy | cost_eth | reduction_pct | avg_wait_min | sla_pct | transactions | mean_batch |
|---|---|---|---|---|---|---|
| P0 Immediate | 1.013 | 0 | 0 | 100 | 8440 | 1 |
| P1 Fixed 12 h | 0.02253 | 97.79 | 124.3 | 100 | 169.3 | 49.86 |
| P2 Threshold (no ML) | 0.02508 | 97.63 | 98.68 | 100 | 229.4 | 36.82 |
| P2b Fee-dep. queue threshold | 0.0274 | 97.41 | 83.54 | 100 | 269.8 | 31.29 |
| P3 Window random | 0.0306 | 97.11 | 112 | 100 | 240.7 | 35.17 |
| P4 Window hour prior | 0.02784 | 97.38 | 110.4 | 100 | 230.4 | 36.72 |
| P5 Window ML | 0.02804 | 97.44 | 110 | 100 | 229.8 | 36.82 |
| P6 Window oracle label | 0.02837 | 97.36 | 108.3 | 100 | 241.1 | 35.13 |
| P7 RL (Q-learning) | 0.02292 | 97.67 | 117.1 | 100 | 194.5 | 45.65 |
| P8 Clairvoyant (future-fee) | 0.02053 | 98.08 | 112.5 | 100 | 193.2 | 43.7 |

## rl_delay_spread
| workload | family | setting | cost_eth | cost_sd_over_rl_seeds | wait_min | wait_sd_over_rl_seeds | transactions |
|---|---|---|---|---|---|---|---|
| bursty 0.2/step + bursts | P7 RL | delay=0.0005 | 0.0119 | 0.0007 | 304.1 | 11.72 | 99.01 |
| bursty 0.2/step + bursts | P7 RL | delay=0.002 | 0.0118 | 0.0002 | 279.9 | 10.19 | 105.7 |
| bursty 0.2/step + bursts | P7 RL | delay=0.005 | 0.0177 | 0.0016 | 189.9 | 12.21 | 163.6 |
| bursty 0.2/step + bursts | P7 RL | delay=0.02 | 0.0306 | 0.007 | 140.3 | 13.91 | 223.7 |
| bursty 0.2/step + bursts | P7 RL | delay=0.05 | 0.0257 | 0.0074 | 166.7 | 33.68 | 205.8 |
| poisson 1.0/step | P7 RL | delay=0.0005 | 0.0228 | 0.0001 | 123.3 | 1.328 | 179.5 |
| poisson 1.0/step | P7 RL | delay=0.002 | 0.0229 | 0.0002 | 121.7 | 1.682 | 179.7 |
| poisson 1.0/step | P7 RL | delay=0.005 | 0.0231 | 0.0003 | 120.5 | 3.76 | 184.1 |
| poisson 1.0/step | P7 RL | delay=0.02 | 0.0235 | 0.0009 | 119.7 | 2.03 | 192.2 |
| poisson 1.0/step | P7 RL | delay=0.05 | 0.028 | 0.0051 | 112.8 | 3.369 | 326.4 |

## simulation_all_runs
_4,980 rows: see simulation_all_runs.csv_

## sla_sensitivity_all
_2,400 rows: see sla_sensitivity_all.csv_

## sla_sensitivity_policies
| sla_h | policy | cost_eth | reduction_pct | avg_wait_min | min_sla_pct | transactions |
|---|---|---|---|---|---|---|
| 6 | P0 Immediate | 1.029 | 0 | 0 | 100 | 8646 |
| 6 | P1 Fixed SLA/2 | 0.03065 | 96.96 | 90.19 | 100 | 235.9 |
| 6 | P2 Threshold (no ML) | 0.02554 | 97.63 | 97.59 | 100 | 234.9 |
| 6 | P2b Fee-dep. queue threshold | 0.02788 | 97.39 | 82.18 | 100 | 276.2 |
| 6 | P3 Window random | 0.03095 | 97.11 | 111.1 | 100 | 247.6 |
| 6 | P4 Window hour prior | 0.02849 | 97.35 | 110 | 100 | 237.2 |
| 6 | P5 Window ML | 0.0285 | 97.42 | 109.8 | 100 | 236.3 |
| 6 | P6 Window oracle label | 0.02902 | 97.33 | 107.8 | 100 | 247.5 |
| 6 | P7 RL (Q-learning) | 0.02783 | 97.22 | 119.3 | 100 | 234.8 |
| 6 | P8 Clairvoyant (future-fee) | 0.02092 | 98.07 | 111.4 | 100 | 198.2 |
| 12 | P0 Immediate | 1.02 | 0 | 0 | 100 | 8580 |
| 12 | P1 Fixed SLA/2 | 0.02285 | 97.7 | 123.2 | 100 | 172.3 |
| 12 | P2 Threshold (no ML) | 0.02528 | 97.63 | 98.3 | 100 | 233.5 |
| 12 | P2b Fee-dep. queue threshold | 0.02764 | 97.4 | 82.58 | 100 | 274.6 |
| 12 | P3 Window random | 0.03084 | 97.1 | 112 | 100 | 244.8 |
| 12 | P4 Window hour prior | 0.02814 | 97.37 | 111.1 | 100 | 235.1 |
| 12 | P5 Window ML | 0.02834 | 97.41 | 110.8 | 100 | 234.5 |
| 12 | P6 Window oracle label | 0.02862 | 97.35 | 108.7 | 100 | 245.7 |
| 12 | P7 RL (Q-learning) | 0.0229 | 97.72 | 118.7 | 100 | 190.2 |
| 12 | P8 Clairvoyant (future-fee) | 0.02069 | 98.07 | 111.7 | 100 | 196.6 |
| 24 | P0 Immediate | 1.013 | 0 | 0 | 100 | 8440 |
| 24 | P1 Fixed SLA/2 | 0.02253 | 97.79 | 124.3 | 100 | 169.3 |
| 24 | P2 Threshold (no ML) | 0.02508 | 97.63 | 98.68 | 100 | 229.4 |
| 24 | P2b Fee-dep. queue threshold | 0.0274 | 97.41 | 83.54 | 100 | 269.8 |
| 24 | P3 Window random | 0.0306 | 97.11 | 112 | 100 | 240.7 |
| 24 | P4 Window hour prior | 0.02784 | 97.38 | 110.4 | 100 | 230.4 |
| 24 | P5 Window ML | 0.02804 | 97.44 | 110 | 100 | 229.8 |
| 24 | P6 Window oracle label | 0.02837 | 97.36 | 108.3 | 100 | 241.1 |
| 24 | P7 RL (Q-learning) | 0.02292 | 97.67 | 117.1 | 100 | 194.5 |
| 24 | P8 Clairvoyant (future-fee) | 0.02053 | 98.08 | 112.5 | 100 | 193.2 |
| 48 | P0 Immediate | 0.9904 | 0 | 0 | 100 | 8155 |
| 48 | P1 Fixed SLA/2 | 0.02199 | 97.8 | 126.5 | 100 | 163.6 |
| 48 | P2 Threshold (no ML) | 0.02453 | 97.64 | 100.4 | 100 | 221.8 |
| 48 | P2b Fee-dep. queue threshold | 0.02677 | 97.41 | 84.74 | 100 | 260.7 |
| 48 | P3 Window random | 0.02985 | 97.1 | 112 | 100 | 232.2 |
| 48 | P4 Window hour prior | 0.02727 | 97.37 | 110.4 | 100 | 222.8 |
| 48 | P5 Window ML | 0.02749 | 97.44 | 110 | 100 | 222.3 |
| 48 | P6 Window oracle label | 0.02776 | 97.36 | 108.3 | 100 | 233 |
| 48 | P7 RL (Q-learning) | 0.02222 | 97.77 | 124.3 | 100 | 175.1 |
| 48 | P8 Clairvoyant (future-fee) | 0.02002 | 98.09 | 112.9 | 100 | 186.7 |

## sla_sensitivity_summary
| SLA (h) | reduction range (%) | P8 gap over best realistic (pp) | cheapest realistic policy | P2b vs P1 | P7 (RL) vs P1 | P5 (ML) vs P4 | min SLA compliance (%) |
|---|---|---|---|---|---|---|---|
| 6 | 96.96-98.07 | 0.44 | P2 | -12.5% [-17.0, -8.2], wait -8.0 min | -7.2% [-16.1, +2.7], wait +29.1 min | -1.5% [-3.9, +1.7], wait -0.2 min | 100 |
| 12 | 97.10-98.07 | 0.35 | P1 | +16.5% [+10.5, +22.3], wait -40.7 min | +0.3% [-1.8, +3.2], wait -4.6 min | -0.6% [-3.2, +2.8], wait -0.3 min | 100 |
| 24 | 97.11-98.08 | 0.29 | P1 | +19.0% [+14.2, +23.9], wait -40.8 min | +6.8% [+1.1, +16.4], wait -7.3 min | -1.0% [-3.4, +2.3], wait -0.3 min | 100 |
| 48 | 97.10-98.09 | 0.29 | P1 | +19.7% [+14.7, +24.6], wait -41.7 min | +3.1% [+0.2, +6.7], wait -2.1 min | -1.3% [-3.9, +2.2], wait -0.4 min | 100 |

## stress_high-fee_fee
| policy | cost_eth | reduction_pct | avg_wait_min | transactions |
|---|---|---|---|---|
| P0 Immediate | 2.616 | 0 | 0 | 8373 |
| P1 Fixed 12 h | 0.05898 | 97.75 | 124.3 | 167.9 |
| P2 Threshold (no ML) | 0.06617 | 97.57 | 100.1 | 224.8 |
| P2b Fee-dep. queue threshold | 0.07316 | 97.32 | 84.76 | 264.8 |
| P3 Window random | 0.08083 | 96.96 | 111.8 | 243.6 |
| P4 Window hour prior | 0.07458 | 97.08 | 110.2 | 229.9 |
| P5 Window ML | 0.07616 | 97.08 | 109.5 | 230.6 |
| P6 Window oracle label | 0.07623 | 97.05 | 108.2 | 240.7 |
| P7 RL (Q-learning) | 0.05944 | 97.72 | 118.2 | 185.2 |
| P8 Clairvoyant (future-fee) | 0.05477 | 97.99 | 112.2 | 192.8 |

## stress_low-fee_fee
| policy | cost_eth | reduction_pct | avg_wait_min | transactions |
|---|---|---|---|---|
| P0 Immediate | 0.118 | 0 | 0 | 8467 |
| P1 Fixed 12 h | 0.002759 | 97.69 | 124.3 | 169.8 |
| P2 Threshold (no ML) | 0.002776 | 97.59 | 97.7 | 232.1 |
| P2b Fee-dep. queue threshold | 0.003285 | 97.21 | 82.83 | 272.6 |
| P3 Window random | 0.003155 | 97.25 | 111.9 | 242.7 |
| P4 Window hour prior | 0.003112 | 97.39 | 110.9 | 229.4 |
| P5 Window ML | 0.003077 | 97.44 | 110.6 | 227.4 |
| P6 Window oracle label | 0.003054 | 97.38 | 107.8 | 245.6 |
| P7 RL (Q-learning) | 0.003207 | 97.44 | 115.8 | 205.7 |
| P8 Clairvoyant (future-fee) | 0.002213 | 98.05 | 112.8 | 192.9 |

## v11_candidates
_9,120 rows: see v11_candidates.csv_

## v11_equal_wait_pairs
| workload | equal_wait_min | pair | meaning | B is | cost diff % (A vs B) | 95% CI (folds) | A cheaper in folds | folds used |
|---|---|---|---|---|---|---|---|---|
| poisson 1.0/step | 80 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | 9.4 | [+3.9, +15.8] | 3/19 | 19 |
| poisson 1.0/step | 80 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 9.4 | [+3.9, +15.8] | 3/19 | 19 |
| poisson 1.0/step | 80 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -16.22 | [-20.5, -12.7] | 20/20 | 20 |
| poisson 1.0/step | 80 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | -9.54 | [-14.2, -5.4] | 17/19 | 19 |
| poisson 1.0/step | 80 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -2.19 | [-5.4, +0.8] | 11/20 | 20 |
| poisson 1.0/step | 80 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -25.76 | [-38.3, -13.7] | 8/9 | 9 |
| poisson 1.0/step | 80 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | -6.04 | [-10.7, -2.4] | 17/20 | 20 |
| poisson 1.0/step | 100 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -1.37 | [-4.5, +1.3] | 10/20 | 20 |
| poisson 1.0/step | 100 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -1.37 | [-4.5, +1.3] | 10/20 | 20 |
| poisson 1.0/step | 100 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -12 | [-16.2, -8.2] | 19/20 | 20 |
| poisson 1.0/step | 100 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 0.39 | [-1.6, +2.5] | 10/20 | 20 |
| poisson 1.0/step | 100 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -0.95 | [-4.8, +2.6] | 9/20 | 20 |
| poisson 1.0/step | 100 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -22.06 | [-33.8, -10.3] | 9/12 | 12 |
| poisson 1.0/step | 100 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | -0.75 | [-5.5, +4.3] | 10/19 | 19 |
| poisson 1.0/step | 120 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -0.14 | [-2.0, +1.8] | 3/8 | 8 |
| poisson 1.0/step | 120 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -0.14 | [-2.0, +1.8] | 3/8 | 8 |
| poisson 1.0/step | 120 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | 2.27 | [-8.7, +14.6] | 7/11 | 11 |
| poisson 1.0/step | 120 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 7.43 | [-2.2, +21.2] | 2/8 | 8 |
| poisson 1.0/step | 120 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 6.32 | [-0.6, +17.2] | 3/10 | 10 |
| poisson 1.0/step | 120 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -4.67 | [-14.7, +7.0] | 6/9 | 9 |
| poisson 1.0/step | 120 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | 2.59 | [-2.8, +9.1] | 4/7 | 7 |
| bursty 0.2/step + bursts | 150 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | 3.17 | [-6.7, +17.9] | 14/17 | 17 |
| bursty 0.2/step + bursts | 150 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2b fee-dep. queue | 0.14 | [-7.1, +10.2] | 11/16 | 16 |
| bursty 0.2/step + bursts | 150 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -24.75 | [-34.0, -17.4] | 16/16 | 16 |
| bursty 0.2/step + bursts | 150 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 3.21 | [-7.4, +11.7] | 6/17 | 17 |
| bursty 0.2/step + bursts | 150 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2b fee-dep. queue | 1.63 | [-6.9, +8.9] | 8/17 | 17 |
| bursty 0.2/step + bursts | 150 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -17.71 | [-24.5, -10.9] | 12/15 | 15 |
| bursty 0.2/step + bursts | 150 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2b fee-dep. queue | -3.28 | [-12.5, +4.2] | 8/14 | 14 |
| bursty 0.2/step + bursts | 200 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -6.81 | [-11.8, -2.6] | 15/17 | 17 |
| bursty 0.2/step + bursts | 200 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2b fee-dep. queue | -2.73 | [-5.8, +0.3] | 14/18 | 18 |
| bursty 0.2/step + bursts | 200 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -28.54 | [-34.4, -23.1] | 18/18 | 18 |
| bursty 0.2/step + bursts | 200 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 3.29 | [-0.0, +6.4] | 3/18 | 18 |
| bursty 0.2/step + bursts | 200 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2b fee-dep. queue | 0.32 | [-3.4, +4.2] | 7/18 | 18 |
| bursty 0.2/step + bursts | 200 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -31.36 | [-37.4, -25.3] | 15/15 | 15 |
| bursty 0.2/step + bursts | 200 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2b fee-dep. queue | 1.89 | [-6.4, +14.5] | 9/16 | 16 |
| bursty 0.2/step + bursts | 250 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -1.04 | [-6.1, +3.6] | 4/7 | 7 |
| bursty 0.2/step + bursts | 250 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -1.04 | [-6.1, +3.6] | 4/7 | 7 |
| bursty 0.2/step + bursts | 250 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -26.64 | [-35.6, -17.3] | 6/6 | 6 |
| bursty 0.2/step + bursts | 250 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 2.12 | [-4.1, +11.2] | 4/6 | 6 |
| bursty 0.2/step + bursts | 250 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 1.05 | [-7.9, +10.5] | 3/6 | 6 |
| bursty 0.2/step + bursts | 250 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -29.36 | [-40.6, -16.4] | 6/7 | 7 |
| bursty 0.2/step + bursts | 250 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | -4.32 | [-14.8, +4.2] | 4/7 | 7 |

## v11_matched_budget_by_fold
_1,080 rows: see v11_matched_budget_by_fold.csv_

## v11_matched_budget_summary
| workload | budget_min | family | test_cost_eth | test_wait_min | folds_feasible_on_val | folds |
|---|---|---|---|---|---|---|
| poisson 1.0/step | 80 | P1 fixed interval | 0.04656 | 59.73 | 20 | 20 |
| poisson 1.0/step | 80 | P2 threshold | 0.0437 | 77.62 | 20 | 20 |
| poisson 1.0/step | 80 | P2b fee-dep. queue | 0.03025 | 78.99 | 20 | 20 |
| poisson 1.0/step | 80 | P2p static pctl (tuned) | 0.02936 | 78.23 | 20 | 20 |
| poisson 1.0/step | 80 | P9 slack-ramp | 0.03428 | 78.12 | 20 | 20 |
| poisson 1.0/step | 80 | P10p wait-value (hour prior) | 0.03296 | 80.83 | 20 | 20 |
| poisson 1.0/step | 80 | P10 wait-value (ML) | 0.02809 | 76.47 | 20 | 20 |
| poisson 1.0/step | 80 | P7 RL | 0.0475 | 79.38 | 12 | 20 |
| poisson 1.0/step | 80 | P10o wait-value (oracle, not deployable) | 0.02743 | 76.45 | 20 | 20 |
| poisson 1.0/step | 100 | P1 fixed interval | 0.02999 | 90.2 | 20 | 20 |
| poisson 1.0/step | 100 | P2 threshold | 0.02501 | 96.66 | 20 | 20 |
| poisson 1.0/step | 100 | P2b fee-dep. queue | 0.026 | 95.62 | 20 | 20 |
| poisson 1.0/step | 100 | P2p static pctl (tuned) | 0.02474 | 97.85 | 20 | 20 |
| poisson 1.0/step | 100 | P9 slack-ramp | 0.02406 | 97.16 | 20 | 20 |
| poisson 1.0/step | 100 | P10p wait-value (hour prior) | 0.02683 | 97.57 | 20 | 20 |
| poisson 1.0/step | 100 | P10 wait-value (ML) | 0.024 | 93.91 | 20 | 20 |
| poisson 1.0/step | 100 | P7 RL | 0.03794 | 89.82 | 18 | 20 |
| poisson 1.0/step | 100 | P10o wait-value (oracle, not deployable) | 0.02445 | 95.68 | 20 | 20 |
| poisson 1.0/step | 120 | P1 fixed interval | 0.02626 | 111.8 | 20 | 20 |
| poisson 1.0/step | 120 | P2 threshold | 0.02305 | 113.8 | 20 | 20 |
| poisson 1.0/step | 120 | P2b fee-dep. queue | 0.0233 | 112.8 | 20 | 20 |
| poisson 1.0/step | 120 | P2p static pctl (tuned) | 0.02286 | 112.5 | 20 | 20 |
| poisson 1.0/step | 120 | P9 slack-ramp | 0.02274 | 114.6 | 20 | 20 |
| poisson 1.0/step | 120 | P10p wait-value (hour prior) | 0.02354 | 116.2 | 20 | 20 |
| poisson 1.0/step | 120 | P10 wait-value (ML) | 0.02383 | 115 | 20 | 20 |
| poisson 1.0/step | 120 | P7 RL | 0.03763 | 90.95 | 19 | 20 |
| poisson 1.0/step | 120 | P10o wait-value (oracle, not deployable) | 0.02255 | 113.5 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P1 fixed interval | 0.01867 | 122.4 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P2 threshold | 0.03024 | 159.2 | 13 | 20 |
| bursty 0.2/step + bursts | 150 | P2b fee-dep. queue | 0.01774 | 153.2 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P2p static pctl (tuned) | 0.01382 | 152.3 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P9 slack-ramp | 0.01272 | 158.3 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P10p wait-value (hour prior) | 0.01861 | 139.6 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P10 wait-value (ML) | 0.01366 | 139 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P7 RL | 0.01849 | 137.7 | 20 | 20 |
| bursty 0.2/step + bursts | 150 | P10o wait-value (oracle, not deployable) | 0.01327 | 151.8 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P1 fixed interval | 0.01785 | 150.2 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P2 threshold | 0.01375 | 205.8 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P2b fee-dep. queue | 0.01115 | 198.7 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P2p static pctl (tuned) | 0.01107 | 205.4 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P9 slack-ramp | 0.01043 | 211.7 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P10p wait-value (hour prior) | 0.01501 | 192 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P10 wait-value (ML) | 0.01082 | 196 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P7 RL | 0.01628 | 195.6 | 20 | 20 |
| bursty 0.2/step + bursts | 200 | P10o wait-value (oracle, not deployable) | 0.0105 | 196.9 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P1 fixed interval | 0.01255 | 215.4 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P2 threshold | 0.009785 | 238.2 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P2b fee-dep. queue | 0.009706 | 248.1 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P2p static pctl (tuned) | 0.009917 | 246.2 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P9 slack-ramp | 0.009296 | 250.1 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P10p wait-value (hour prior) | 0.01236 | 252.6 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P10 wait-value (ML) | 0.009343 | 246.2 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P7 RL | 0.01076 | 251.9 | 20 | 20 |
| bursty 0.2/step + bursts | 250 | P10o wait-value (oracle, not deployable) | 0.009113 | 255.6 | 20 | 20 |

## v11_paired_comparisons
| workload | budget_min | pair | meaning | B is | cost diff % (A vs B) | 95% CI (folds) | A cheaper in folds | wait diff (min) |
|---|---|---|---|---|---|---|---|---|
| poisson 1.0/step | 80 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | 9.72 | [+2.7, +18.1] | 6/20 | -0.1 |
| poisson 1.0/step | 80 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 9.72 | [+2.7, +18.1] | 6/20 | -0.1 |
| poisson 1.0/step | 80 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -9.55 | [-17.2, -1.9] | 15/20 | -4.4 |
| poisson 1.0/step | 80 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | -5.84 | [-14.3, +2.0] | 12/20 | -1.7 |
| poisson 1.0/step | 80 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 1.56 | [-6.6, +10.2] | 11/20 | -1.8 |
| poisson 1.0/step | 80 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -27.1 | [-40.8, -13.3] | 16/20 | -2.9 |
| poisson 1.0/step | 80 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | -0.8 | [-10.2, +10.8] | 11/20 | -1.8 |
| poisson 1.0/step | 100 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -1.04 | [-4.7, +2.2] | 10/20 | -0.7 |
| poisson 1.0/step | 100 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -1.04 | [-4.7, +2.2] | 10/20 | -0.7 |
| poisson 1.0/step | 100 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -10.25 | [-14.6, -5.7] | 18/20 | -3.7 |
| poisson 1.0/step | 100 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 1.93 | [-1.4, +5.5] | 9/20 | -3.2 |
| poisson 1.0/step | 100 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 0.89 | [-4.1, +5.9] | 9/20 | -3.9 |
| poisson 1.0/step | 100 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -15.91 | [-28.7, -3.7] | 13/20 | 4.1 |
| poisson 1.0/step | 100 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | -0.24 | [-4.5, +4.2] | 9/20 | -2.2 |
| poisson 1.0/step | 120 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -0.64 | [-2.4, +1.2] | 8/20 | 2.1 |
| poisson 1.0/step | 120 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -0.64 | [-2.4, +1.2] | 8/20 | 2.1 |
| poisson 1.0/step | 120 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | 0.39 | [-10.9, +11.9] | 10/20 | -1.2 |
| poisson 1.0/step | 120 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 3.58 | [-6.8, +14.8] | 7/20 | 0.4 |
| poisson 1.0/step | 120 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 2.7 | [-7.2, +13.8] | 8/20 | 2.5 |
| poisson 1.0/step | 120 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -20.41 | [-31.6, -9.9] | 18/20 | 24.1 |
| poisson 1.0/step | 120 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | 1.39 | [-3.6, +6.3] | 9/20 | 1 |
| bursty 0.2/step + bursts | 150 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -9.12 | [-14.3, -2.3] | 19/20 | 6 |
| bursty 0.2/step + bursts | 150 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -9.12 | [-14.3, -2.3] | 19/20 | 6 |
| bursty 0.2/step + bursts | 150 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -25.53 | [-33.8, -16.6] | 18/20 | -0.6 |
| bursty 0.2/step + bursts | 150 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 21.56 | [+9.9, +32.3] | 3/20 | -19.3 |
| bursty 0.2/step + bursts | 150 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 8.52 | [-0.6, +18.0] | 10/20 | -13.3 |
| bursty 0.2/step + bursts | 150 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -17.12 | [-25.0, -8.8] | 16/20 | 1.4 |
| bursty 0.2/step + bursts | 150 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | 2.97 | [-4.1, +10.5] | 8/20 | -0.5 |
| bursty 0.2/step + bursts | 200 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -2 | [-9.3, +6.7] | 12/20 | 6.3 |
| bursty 0.2/step + bursts | 200 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | -2 | [-9.3, +6.7] | 12/20 | 6.3 |
| bursty 0.2/step + bursts | 200 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -27.94 | [-37.3, -18.3] | 18/20 | 4.1 |
| bursty 0.2/step + bursts | 200 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | 4.99 | [-3.4, +14.2] | 8/20 | -15.6 |
| bursty 0.2/step + bursts | 200 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2p static pctl (tuned) | 1.64 | [-7.3, +11.3] | 11/20 | -9.3 |
| bursty 0.2/step + bursts | 200 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -23.29 | [-33.1, -13.6] | 16/20 | 0.5 |
| bursty 0.2/step + bursts | 200 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2p static pctl (tuned) | -0.07 | [-8.5, +8.8] | 13/20 | -8.5 |
| bursty 0.2/step + bursts | 250 | P9 vs P2p | slack-awareness alone | P2p static pctl (tuned) | -8.12 | [-14.2, -2.2] | 17/20 | 3.9 |
| bursty 0.2/step + bursts | 250 | P9 vs best static rule | P9 against the best of P1/P2/P2b/P2p | P2b fee-dep. queue | -2.9 | [-9.9, +4.5] | 16/20 | 2.1 |
| bursty 0.2/step + bursts | 250 | P10 vs P10p | ML forecast vs hour-of-day forecast | P10p wait-value (hour prior) | -20.23 | [-30.3, -10.5] | 19/20 | -6.4 |
| bursty 0.2/step + bursts | 250 | P10 vs P9 | ML on top of slack-awareness | P9 slack-ramp | -0.57 | [-4.5, +3.6] | 10/20 | -3.9 |
| bursty 0.2/step + bursts | 250 | P10 vs best static rule | P10 against the best of P1/P2/P2b/P2p | P2b fee-dep. queue | -3.78 | [-11.3, +3.3] | 13/20 | -1.8 |
| bursty 0.2/step + bursts | 250 | P10 vs P7 RL | decision-aligned ML vs tabular RL | P7 RL | -15 | [-21.5, -8.1] | 16/20 | -5.6 |
| bursty 0.2/step + bursts | 250 | P10o vs best static rule | ceiling of the trigger family (true value of waiting) | P2b fee-dep. queue | -9.27 | [-18.4, +1.3] | 17/20 | 7.6 |

## v11_wait_value_forecast_skill
| horizon_h | mae_ml | mae_hour_prior | folds_ml_better | folds | skill_vs_hour_prior_pct | skill 95% CI (folds) |
|---|---|---|---|---|---|---|
| 1 | 0.1632 | 0.1984 | 20 | 20 | 17.75 | [+15.4, +19.3] |
| 3 | 0.2021 | 0.2871 | 20 | 20 | 29.62 | [+26.8, +31.7] |
| 6 | 0.2248 | 0.3597 | 20 | 20 | 37.51 | [+34.9, +39.7] |
| 12 | 0.246 | 0.4299 | 20 | 20 | 42.77 | [+40.5, +45.0] |
| 24 | 0.275 | 0.4837 | 20 | 20 | 43.15 | [+40.4, +45.8] |

## v11_wait_value_forecast_skill_by_fold
| fold | horizon_h | mae_ml | mae_hour_prior | ml_better | skill_pct |
|---|---|---|---|---|---|
| 2025-01-01 | 1 | 0.1331 | 0.1377 | True | 3.32 |
| 2025-01-01 | 3 | 0.1712 | 0.1956 | True | 12.51 |
| 2025-01-01 | 6 | 0.1944 | 0.2546 | True | 23.62 |
| 2025-01-01 | 12 | 0.2 | 0.3174 | True | 37 |
| 2025-01-01 | 24 | 0.2406 | 0.365 | True | 34.1 |
| 2025-02-01 | 1 | 0.1274 | 0.164 | True | 22.32 |
| 2025-02-01 | 3 | 0.1576 | 0.2425 | True | 35 |
| 2025-02-01 | 6 | 0.1806 | 0.298 | True | 39.39 |
| 2025-02-01 | 12 | 0.2179 | 0.3535 | True | 38.37 |
| 2025-02-01 | 24 | 0.2652 | 0.4158 | True | 36.23 |
| 2025-03-01 | 1 | 0.12 | 0.1508 | True | 20.45 |
| 2025-03-01 | 3 | 0.1438 | 0.2212 | True | 34.98 |
| 2025-03-01 | 6 | 0.1536 | 0.2671 | True | 42.48 |
| 2025-03-01 | 12 | 0.1806 | 0.3106 | True | 41.86 |
| 2025-03-01 | 24 | 0.2209 | 0.3522 | True | 37.27 |
| 2025-04-01 | 1 | 0.1476 | 0.1807 | True | 18.28 |
| 2025-04-01 | 3 | 0.1901 | 0.2792 | True | 31.92 |
| 2025-04-01 | 6 | 0.2225 | 0.3631 | True | 38.72 |
| 2025-04-01 | 12 | 0.2411 | 0.4075 | True | 40.82 |
| 2025-04-01 | 24 | 0.2594 | 0.4418 | True | 41.29 |
| 2025-05-01 | 1 | 0.1753 | 0.2048 | True | 14.38 |
| 2025-05-01 | 3 | 0.2288 | 0.3012 | True | 24.04 |
| 2025-05-01 | 6 | 0.2542 | 0.3845 | True | 33.89 |
| 2025-05-01 | 12 | 0.3003 | 0.4879 | True | 38.45 |
| 2025-05-01 | 24 | 0.3402 | 0.5627 | True | 39.54 |
| 2025-06-01 | 1 | 0.1745 | 0.2048 | True | 14.77 |
| 2025-06-01 | 3 | 0.2229 | 0.3022 | True | 26.23 |
| 2025-06-01 | 6 | 0.2585 | 0.3854 | True | 32.92 |
| 2025-06-01 | 12 | 0.3156 | 0.4928 | True | 35.96 |
| 2025-06-01 | 24 | 0.3651 | 0.5992 | True | 39.07 |
| 2025-07-01 | 1 | 0.1594 | 0.1762 | True | 9.531 |
| 2025-07-01 | 3 | 0.2217 | 0.2701 | True | 17.91 |
| 2025-07-01 | 6 | 0.2757 | 0.3588 | True | 23.15 |
| 2025-07-01 | 12 | 0.3386 | 0.4926 | True | 31.26 |
| 2025-07-01 | 24 | 0.4239 | 0.6228 | True | 31.94 |
| 2025-08-01 | 1 | 0.1483 | 0.1808 | True | 18 |
| 2025-08-01 | 3 | 0.1749 | 0.2522 | True | 30.67 |
| 2025-08-01 | 6 | 0.1869 | 0.3116 | True | 40 |
| 2025-08-01 | 12 | 0.1981 | 0.3743 | True | 47.07 |
| 2025-08-01 | 24 | 0.2297 | 0.421 | True | 45.44 |
| 2025-09-01 | 1 | 0.156 | 0.1863 | True | 16.27 |
| 2025-09-01 | 3 | 0.2026 | 0.2854 | True | 29.01 |
| 2025-09-01 | 6 | 0.2415 | 0.3987 | True | 39.43 |
| 2025-09-01 | 12 | 0.2749 | 0.5157 | True | 46.71 |
| 2025-09-01 | 24 | 0.2694 | 0.5614 | True | 52.02 |
| 2025-10-01 | 1 | 0.1607 | 0.1993 | True | 19.38 |
| 2025-10-01 | 3 | 0.2188 | 0.3137 | True | 30.27 |
| 2025-10-01 | 6 | 0.2503 | 0.4186 | True | 40.21 |
| 2025-10-01 | 12 | 0.2667 | 0.5171 | True | 48.41 |
| 2025-10-01 | 24 | 0.269 | 0.5616 | True | 52.1 |
| 2025-11-01 | 1 | 0.1871 | 0.2282 | True | 18.01 |
| 2025-11-01 | 3 | 0.2567 | 0.3566 | True | 28.01 |
| 2025-11-01 | 6 | 0.2902 | 0.4657 | True | 37.69 |
| 2025-11-01 | 12 | 0.3111 | 0.5684 | True | 45.27 |
| 2025-11-01 | 24 | 0.3327 | 0.6426 | True | 48.23 |
| 2025-12-01 | 1 | 0.1525 | 0.1856 | True | 17.84 |
| 2025-12-01 | 3 | 0.1955 | 0.2754 | True | 29.02 |
| 2025-12-01 | 6 | 0.202 | 0.3327 | True | 39.28 |
| 2025-12-01 | 12 | 0.2047 | 0.3833 | True | 46.58 |
| 2025-12-01 | 24 | 0.258 | 0.4242 | True | 39.19 |
| 2026-01-01 | 1 | 0.1764 | 0.2183 | True | 19.18 |
| 2026-01-01 | 3 | 0.2011 | 0.3095 | True | 35.02 |
| 2026-01-01 | 6 | 0.2058 | 0.3816 | True | 46.08 |
| 2026-01-01 | 12 | 0.2018 | 0.4185 | True | 51.79 |
| 2026-01-01 | 24 | 0.221 | 0.4444 | True | 50.26 |
| 2026-02-01 | 1 | 0.169 | 0.2064 | True | 18.16 |
| 2026-02-01 | 3 | 0.2105 | 0.3004 | True | 29.93 |
| 2026-02-01 | 6 | 0.223 | 0.3692 | True | 39.59 |
| 2026-02-01 | 12 | 0.2097 | 0.4131 | True | 49.23 |
| 2026-02-01 | 24 | 0.23 | 0.454 | True | 49.34 |
| 2026-03-01 | 1 | 0.1716 | 0.2089 | True | 17.86 |
| 2026-03-01 | 3 | 0.2053 | 0.3028 | True | 32.21 |
| 2026-03-01 | 6 | 0.2162 | 0.3716 | True | 41.84 |
| 2026-03-01 | 12 | 0.2172 | 0.4335 | True | 49.91 |
| 2026-03-01 | 24 | 0.2079 | 0.4642 | True | 55.21 |
| 2026-04-01 | 1 | 0.2088 | 0.251 | True | 16.81 |
| 2026-04-01 | 3 | 0.2524 | 0.3599 | True | 29.88 |
| 2026-04-01 | 6 | 0.2876 | 0.4352 | True | 33.92 |
| 2026-04-01 | 12 | 0.3264 | 0.5248 | True | 37.8 |
| 2026-04-01 | 24 | 0.3685 | 0.6205 | True | 40.61 |
| 2026-05-01 | 1 | 0.1861 | 0.2294 | True | 18.89 |
| 2026-05-01 | 3 | 0.2092 | 0.3037 | True | 31.14 |
| 2026-05-01 | 6 | 0.221 | 0.3611 | True | 38.79 |
| 2026-05-01 | 12 | 0.2442 | 0.4102 | True | 40.48 |
| 2026-05-01 | 24 | 0.2608 | 0.4349 | True | 40.03 |
| 2026-06-01 | 1 | 0.1723 | 0.2255 | True | 23.6 |
| 2026-06-01 | 3 | 0.1906 | 0.2949 | True | 35.38 |
| 2026-06-01 | 6 | 0.2085 | 0.3539 | True | 41.08 |
| 2026-06-01 | 12 | 0.2232 | 0.3942 | True | 43.38 |
| 2026-06-01 | 24 | 0.2556 | 0.436 | True | 41.38 |
| 2026-07-01 | 1 | 0.1789 | 0.227 | True | 21.18 |
| 2026-07-01 | 3 | 0.194 | 0.2881 | True | 32.67 |
| 2026-07-01 | 6 | 0.2043 | 0.3373 | True | 39.45 |
| 2026-07-01 | 12 | 0.216 | 0.3826 | True | 43.54 |
| 2026-07-01 | 24 | 0.2278 | 0.4082 | True | 44.18 |
| 2026-08-01 | 1 | 0.1583 | 0.2021 | True | 21.66 |
| 2026-08-01 | 3 | 0.1939 | 0.2876 | True | 32.56 |
| 2026-08-01 | 6 | 0.2189 | 0.3462 | True | 36.78 |
| 2026-08-01 | 12 | 0.2326 | 0.3996 | True | 41.78 |
| 2026-08-01 | 24 | 0.2536 | 0.4406 | True | 42.43 |

## v12_cost_vs_wait_by_fold
_2,561 rows: see v12_cost_vs_wait_by_fold.csv_

## v12_wait_value_seed_by_fold
_500 rows: see v12_wait_value_seed_by_fold.csv_

## v12_wait_value_seed_variance
| horizon_h | skill_mean_pct | skill_sd_pct | skill_min_pct | skill_max_pct | mae_ml_mean | mae_ml_sd | n_seeds |
|---|---|---|---|---|---|---|---|
| 1 | 17.81 | 0.06228 | 17.75 | 17.88 | 0.163 | 0.0001236 | 5 |
| 3 | 29.69 | 0.06785 | 29.62 | 29.78 | 0.2019 | 0.0001948 | 5 |
| 6 | 37.54 | 0.05629 | 37.46 | 37.61 | 0.2247 | 0.0002025 | 5 |
| 12 | 42.8 | 0.08502 | 42.7 | 42.89 | 0.2459 | 0.0003655 | 5 |
| 24 | 43.05 | 0.09074 | 42.96 | 43.15 | 0.2755 | 0.0004389 | 5 |

## window_per_fold
| fold | selected | hour prior | ML beats hour prior |
|---|---|---|---|
| 2025-01-01 | 33.87 | 37.08 | True |
| 2025-02-01 | 81.56 | 102.5 | True |
| 2025-03-01 | 13.88 | 15.53 | True |
| 2025-04-01 | 12.66 | 11.57 | False |
| 2025-05-01 | 13.59 | 11.26 | False |
| 2025-06-01 | 12.89 | 15.07 | True |
| 2025-07-01 | 20.02 | 20.1 | True |
| 2025-08-01 | 13.8 | 11.82 | False |
| 2025-09-01 | 6.331 | 6.585 | True |
| 2025-10-01 | 36.53 | 24.93 | False |
| 2025-11-01 | 13.28 | 14.58 | True |
| 2025-12-01 | 73.92 | 74.33 | True |
| 2026-01-01 | 6.821 | 6.377 | False |
| 2026-02-01 | 22.75 | 20.16 | False |
| 2026-03-01 | 20.34 | 17.62 | False |
| 2026-04-01 | 30.54 | 29.57 | False |
| 2026-05-01 | 12.79 | 13.18 | True |
| 2026-06-01 | 17.12 | 18.76 | True |
| 2026-07-01 | 13.65 | 14.14 | True |
| 2026-08-01 | 18.7 | 20.49 | True |

## window_walkforward
| method | accuracy | top2_acc | regret_pct_of_random | 95% CI | diff vs hour prior (pts) |
|---|---|---|---|---|---|
| random (expected) | 0.25 | 0.5 | 100 | - | - |
| yesterday | 0.4671 | nan | 51.47 | [35.6, 67.7] | +20.91 [+11.87, +30.20] |
| hour prior | 0.5623 | nan | 30.53 | [16.7, 44.6] | - |
| logreg | 0.5664 | 0.8847 | 30.42 | [17.4, 44.2] | -0.02 [-3.59, +3.32] |
| xgboost | 0.5715 | 0.8878 | 28.7 | [16.9, 41.4] | -1.60 [-7.38, +3.80] |
| selected | 0.5679 | 0.8841 | 28.19 | [16.4, 40.9] | -2.11 [-7.79, +3.32] |
| oracle | 1 | 1 | 0 | - | - |

## workload_reference_policies
| workload | setting | cost_eth | avg_wait_min | transactions | reduction_pct |
|---|---|---|---|---|---|
| bursty 0.2/step + bursts | P0 Immediate | 0.4125 | 0 | 2957 | 0 |
| bursty 0.2/step + bursts | P1 Fixed 12 h | 0.01186 | 233.3 | 80.25 | 97.12 |
| bursty 0.2/step + bursts | P2 Threshold (no ML) | 0.01305 | 174.9 | 170.1 | 96.83 |
| bursty 0.2/step + bursts | P2b Fee-dep. queue threshold | 0.0142 | 142 | 184.9 | 96.56 |
| bursty 0.2/step + bursts | P3 Window random | 0.01342 | 257.4 | 106.8 | 96.75 |
| bursty 0.2/step + bursts | P4 Window hour prior | 0.0113 | 273.3 | 108.1 | 97.26 |
| bursty 0.2/step + bursts | P5 Window ML | 0.01087 | 272 | 108 | 97.37 |
| bursty 0.2/step + bursts | P6 Window oracle label | 0.01263 | 250.6 | 120.3 | 96.94 |
| bursty 0.2/step + bursts | P8 Clairvoyant (future-fee) | 0.00987 | 214.1 | 112.9 | 97.61 |
| poisson 1.0/step | P0 Immediate | 1.013 | 0 | 8440 | 0 |
| poisson 1.0/step | P1 Fixed 12 h | 0.02253 | 124.3 | 169.3 | 97.78 |
| poisson 1.0/step | P2 Threshold (no ML) | 0.02508 | 98.68 | 229.4 | 97.52 |
| poisson 1.0/step | P2b Fee-dep. queue threshold | 0.0274 | 83.54 | 269.8 | 97.29 |
| poisson 1.0/step | P3 Window random | 0.0306 | 112 | 240.7 | 96.98 |
| poisson 1.0/step | P4 Window hour prior | 0.02784 | 110.4 | 230.4 | 97.25 |
| poisson 1.0/step | P5 Window ML | 0.02804 | 110 | 229.8 | 97.23 |
| poisson 1.0/step | P6 Window oracle label | 0.02837 | 108.3 | 241.1 | 97.2 |
| poisson 1.0/step | P8 Clairvoyant (future-fee) | 0.02053 | 112.5 | 193.2 | 97.97 |
