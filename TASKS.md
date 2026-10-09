# Tasks: write the code yourself, then ask AI to review it

Tick a box only when the code runs and you could explain every line to an interviewer.

## Week 1 · Parse (Mon 10/5 – Sun 10/11)
- [ ] Copy `raw_data_steel` into `data/raw/`
- [ ] `notebooks/01_parse.ipynb`: read ONE file with `pd.read_csv(path, sep="\t", header=None, skiprows=3, encoding="cp949", names=["i","load_kgf","torque_Nm"])`
- [ ] Plot load vs. sample index and torque vs. sample index for that one file. Describe the shape in one sentence.
- [ ] Write `parse_name(path)` → `(config, target_torque, repeat)` using `re`
- [ ] Loop over all 67 files → one DataFrame with columns `config, target_torque, repeat, peak_torque_Nm, peak_load_N`
- [ ] Save it as `data/processed/runs_summary.csv` (this small file *can* go on GitHub)

## Week 2 · Explore (10/12 – 10/18)
- [ ] `notebooks/02_explore.ipynb`: add `K = peak_torque / (peak_load_N * d)`
- [ ] Group by `config, target_torque` → mean, std and count of K
- [ ] Figure: K vs. target torque, one line per config, error bars = std. Save to `figures/`
- [ ] Check that the 30–90 N·m plateau (K ≈ 0.24) and the rise at 100 N·m appear in your own plot
- [ ] Write the first 3 bullets of *Results* in the README

## Week 3 · Physics vs. ML (10/19 – 10/25)
- [ ] `notebooks/03_models.ipynb`: target = `peak_load_N`. Features: `peak_torque_Nm`, `config` (one-hot), lubrication flag
- [ ] Baseline: physics prediction `F = T / (K·d)` using the thesis K
- [ ] Linear regression → random forest → LightGBM
- [ ] Validation: `GroupKFold` grouped by `(config, target_torque)` so repeats don't leak between train and test
- [ ] Table: MAE (kN) for each model. Is ML actually better? Why or why not? (With 67 rows, "no" is a fine and honest answer.)

## Week 4 · Explain + publish (10/26 – 11/1)
- [ ] SHAP summary plot for the best model. Does it lean on torque and config the way the mechanics says it should?
- [ ] Fill in every *TODO* in README.md, including *What failed*
- [ ] Ask Prof. Kim (email) whether you may publish the raw data or only the summary
- [ ] `git init`, first commit, create the GitHub repo, push
- [ ] Add the repo link to LinkedIn Featured, Saramin and JobKorea 포트폴리오

## Interview questions this project must let you answer
- Why does K rise at 100 N·m, physically?
- Why GroupKFold instead of a random split?
- With only 67 runs, how do you know the ML model isn't overfitting?
- What would you measure differently if you redid the experiment?
