# Exit-Capacity-and-Congestion-in-Simulated-Pedestrian-Evacuation-A-Factorial-Comparison-Flow-Models
# Pedestrian Evacuation Simulation, Version 2

**Author:** Christian Somtoo Obiechina
**Status:** Research prototype. Synthetic simulation output. Not calibrated or validated against observed evacuation data.

## What is in this folder

- `evacuation_simulation_v2.ipynb`: executed notebook (outputs stored)
- `results/`: replicate data, scenario summary, verification checks, hypothesis tests, factorial regressions, sensitivity analysis, figures and run metadata

## Design

- Two exit-flow models: `unconstrained` (version 1 behaviour) and `capacity` (exit serves an assumed flow of 1.3 persons per metre of width per second).
- Factorial design: crowd size (40, 80), exit width (0.8, 1.2, 1.6 m), desired speed (1.0, 1.3 m/s), obstacle (absent, present), by model. 96 conditions in total, 20 seeded replicates each, 1,920 main simulations.
- Sensitivity analysis: five repulsion and separation-radius variants, both models, 400 simulations.

## Main findings (within these models)

| Hypothesis | Unconstrained model | Capacity model |
|---|---|---|
| H1: wider exit reduces t90 | Supported. Median effect −0.55 s (CI −0.60 to −0.50) | Supported. Median effect −25.6 s (CI −34.0 to −17.0) |
| H2: larger crowd increases t90 | Supported. +0.85 s | Supported. +22.7 s |
| H3: obstacle worsens t90 | Supported. +0.75 s | Supported but small. +0.10 s |

- **Verification:** reproducibility, boundary, count, horizon and single-agent checks pass.
- **Unconstrained model:** exceeds the assumed exit flow limit in 99.8% of runs. The model has no physical capacity limit, so its exit-width effect is small and depends on the interaction settings.
- **Capacity model:** narrow-exit t90 median is about 71 s, close to the simple flow estimate 0.9 × 80 ÷ (1.3 × 0.8) ≈ 69 s. The width effect is large and stable across sensitivity variants.
- **Sensitivity:** the sign of the width effect is the same in all five variants for both models. The size of the effect under the unconstrained model changes from −0.3 s to −1.0 s, so that model's magnitude is not robust.

## Cautions for any write-up

1. The flow rate 1.3 persons per metre per second is an assumption. Verify it against a cited source before use.
2. The capacity model's flow limit holds by construction. The check confirms the implementation, not the realism of the assumption.
3. Replicates vary only in placement and individual speed. Confidence intervals are therefore very narrow and should not be read as real-world uncertainty.
4. Neither model includes way-finding, route choice, pushing, or behavioural heterogeneity.

## Reproduce

```bash
pip install numpy pandas scipy matplotlib
python evacuation_simulation_v2.py   # or run the notebook
```
