# Torque–Preload Analysis of a Hydrogen Valve Bolted Joint

> **Status:** in progress. Sections marked *TODO* get filled in as the work is done.

Real tightening-test data from my M.S. research at Pusan National University, analysed with Python:
from raw instrument files → clean dataset → nut factor with uncertainty → physics model vs. machine learning.

## Problem

The outlet port of an 87.5 MPa hydrogen valve is sealed by a hollow bolt that compresses a confined
polyimide (PI) ring. That ring adds a third friction interface the classical two-interface
nut-factor model ignores, so the usual torque spec can't be trusted.

**Questions this repo answers**

1. How does the nut factor *K* change with tightening torque, and how much does it scatter between repeats?
2. How much of the input torque turns into clamp force, and where does it start leaking into thread friction?
3. Can a data-driven model predict clamp force better than the physics model, and does it rely on the same variables the mechanics predicts?

## Data

67 tightening runs recorded by a load cell and torque meter (one text file per run, ~13,500 samples each).

| Folder | Runs | What it tests |
|---|---|---|
| `Config_A` | 21 | *TODO: describe configuration A* |
| `Config_B` | 18 | *TODO: describe configuration B* |
| `Config_C` | 18 | *TODO: describe configuration C* |
| `Sequential_lubrication` | 10 | *TODO: describe the μ_ss / μ_b lubrication series* |

Target torques: 30, 50, 70, 90, 100 N·m, with 3–5 repeats each. File format: [`data/README.md`](data/README.md).

The raw files are not published yet (see *Data availability*). `data/processed/` will hold a cleaned summary table.

## Approach

1. **Parse.** Read every raw file (header in CP949 Korean encoding), and convert load from kgf to N.
2. **Summarise.** For each run: peak torque, peak clamp force, and *K = T / (F·d)*.
3. **Explore.** *K* vs. torque per configuration, with repeat scatter as error bars.
4. **Physics model.** The three-interface nut-factor model from the thesis.
5. **ML model.** Linear regression → random forest → gradient boosting (LightGBM), with a validation split that keeps all repeats of one run together.
6. **Explain.** SHAP values: does the model agree with the mechanics?

## Results

*TODO: the K-vs-torque figure, a summary table, and the physics-vs-ML error table (MAE in kN).*

## What failed / limitations

*TODO: be honest here. It's the section engineers read first.*

## How to run

```bash
python -m venv .venv
.venv\Scripts\activate
pip install pandas numpy matplotlib seaborn scikit-learn lightgbm shap jupyter
jupyter notebook notebooks/
```

## Data availability

Raw data belongs to MI Lab, Pusan National University. *TODO: publish once Prof. Kim Hwa Young approves, or publish only the processed summary table.*

## Author

Enkh-Amar Ganbat · M.S. Mechanical Engineering (Control & Automation), Pusan National University
