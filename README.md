# reliability-first-physics-data-science
This GitHub repository is a reproducible, teaching-ready set of scripts that shows how to do data science responsibly for physics, astronomy, and mathematics. It demonstrates how results can look “too good” when you test models with simple random splits, and how performance often drops when you use more realistic tests, like group-based splits and out-of-distribution data. It also shows how to measure and improve trust in predictions using calibration, uncertainty estimates, and risk–coverage curves, so you can decide when a model should answer and when it should defer. Finally, it includes clear proof-of-concept implementations of Bayesian optimisation and multiobjective optimisation to efficiently choose the next best experiments when each experiment is expensive, producing interpretable plots, tables, and decision-style reports.

Reproducible scripts for reliability-critical data science in physics-facing domains, covering time-series modelling, calibration under dataset shift, and Bayesian optimisation, including multiobjective Pareto analysis.

# Reliability-Critical Data Science for Physics, Astronomy, and Mathematics  
**Benchmarking under dataset shift, uncertainty-aware decision support, and Bayesian optimisation for expensive simulators**

This repository is a reproducible, teaching-ready proof-of-concept that demonstrates how to build **decision-grade** data science workflows for Physics, Astronomy, and Mathematics. It focuses on three practical capabilities that matter in real deployment:  
1) **Time-series learning** on light-curve style data (regression + classification),  
2) **Reliability under realistic evaluation splits** (random vs group vs out-of-distribution), including **calibration** and **risk–coverage** selective prediction,  
3) **Sequential design** for expensive black-box objectives using **Gaussian Process Bayesian Optimisation (BO)** and **Multiobjective Bayesian Optimisation (MOBO, MOBO++)** with Pareto, hypervolume, and epsilon-constraint decision views.

## What you get

### Scripts demonstrated
- **Time-series prediction**: feature-to-target regression and classification with multiple evaluation regimes.
- **Reliability diagnostics**: AUC summaries, **reliability diagrams**, **risk–coverage** curves, and uncertainty–error coupling.
- **Bayesian optimisation**: convergence curves, GP surrogate mean/uncertainty maps, acquisition maps, BO vs random baselines.
- **Multiobjective BO (MOBO++)**: Pareto front, Pareto ranks, hypervolume curves, hypervolume contributions, epsilon-constraint trade-offs, optional OOD regime shift checks.

## Repository outputs (figures and tables)

All outputs are written to `figures/` and `tables/` directories (or to an experiment `--outdir` containing those folders).

### Figures (PNG)
**Reliability and time-series**
- `example_lightcurves.png`  
- `example_series_153.png`, `example_series_260.png`, `example_series_ood_71.png`, `example_series_ood_86.png`  
- `period_regression_group.png`  
- `auc_summary.png`  
- `reliability_random_split.png`, `reliability_group_split.png`, `reliability_ood.png`  
- `risk_coverage_random.png`, `risk_coverage_group.png`, `risk_coverage_ood.png`  
- `uncertainty_gamma_std_vs_error.png`, `uncertainty_omega0_std_vs_error.png`  
- `scatter_baseline_gamma.png`, `scatter_baseline_omega0.png`  
- `scatter_rf_gamma.png`, `scatter_rf_omega0.png`  
- `scatter_gpr_gamma.png`, `scatter_gpr_omega0.png`

**Single-objective BO (GP Bayesian optimisation)**
- `convergence.png`  
- `gp_mean_map.png`  
- `gp_std_map.png`  
- `acquisition_map.png`  
- `bo_vs_random.png`

**Multiobjective optimisation (MOBO / MOBO++)**
- `pareto_front.png`  
- `pareto_ranks.png`  
- `hypervolume_curve.png`  
- `hv_contribution_top.png`  
- `epsilon_constraint_curve.png`  
- `design_space_pareto.png`

### Tables (CSV)
**Time-series tasks**
- `timeseries_preview.csv`  
- `lightcurves_preview.csv`  
- `labels_table.csv`  
- `regression_metrics.csv`  
- `classification_metrics.csv`  
- `group_split_metrics.csv`  
- `ood_metrics.csv`

**Single-objective BO**
- `bo_trace.csv`  
- `metrics_report.json`

**MOBO / MOBO++**
- `mobo_trace.csv`  
- `pareto_front.csv`  
- `mobo_plus_trace.csv`  
- `pareto_front_plus.csv`  
- `hypervolume_trace.csv`  
- `epsilon_constraint_report.csv`  
- `metrics_report.json`

## Quickstart

### 1) Create an environment
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install numpy pandas matplotlib scikit-learn

### 2) Run the single-objective BO proof-of-concept
python uh_bayesopt_physics_poc.py --outdir uh_bo_outputs --acq ei --budget 60
Outputs:
	•	Figures in uh_bo_outputs/figures/
	•	Tables in uh_bo_outputs/tables/

### 3) Run MOBO++ (performance vs cost)
python uh_mobo_plus_poc.py --outdir uh_mobo_plus --budget 100 --batch_size 4
Outputs:
	•	Figures in uh_mobo_plus/figures/
	•	Tables in uh_mobo_plus/tables/

## Reproducibility
All scripts accept a fixed random seed.
Examples:
python uh_bayesopt_physics_poc.py --seed 42
python uh_mobo_plus_poc.py --seed 42

## Project structure 
```
├── bayesopt_physics_poc.py
├── mobo_plus_poc.py
├── figures/
├── tables/
└── README.md
```
## Citation
**Petalcorin, M. I. R. (2026)**. reliability-first-physics-data-science: Reliability-Critical Data Science for Physics, Astronomy, and Mathematics. GitHub Repository: https://github.com/mpetalcorin/reliability-first-physics-data-science

# Model Card, Reliability-Critical Data Science for Physics/Astronomy/Mathematics (PoC)
## 1. Model details
**Model name:** Reliability-Critical Data Science PoC Models (Time-series + BO/MOBO)  
**Model type:** Classical ML baselines and Gaussian Process models used for (i) supervised learning on time-series style data and (ii) Bayesian optimisation / multiobjective Bayesian optimisation.  
**Primary components:**
- **Time-series prediction models:** baseline predictors, Random Forest (RF), Gaussian Process Regression (GPR) style regressors, and a probabilistic classifier for label prediction (exact estimator depends on notebook/script configuration).
- **Optimisation models:** **GaussianProcessRegressor** surrogate(s) for Bayesian optimisation (single-objective) and MOBO++ (multiobjective with two GP surrogates, one per objective).

**Intended users:** educators, students, researchers, and applied practitioners building reliability-first workflows in Physics/Astronomy/Mathematics.  
**License:** add your repository license (e.g., MIT/BSD/Apache-2.0).

## 2. Intended use
### Intended use cases
- Teaching **evaluation design** beyond i.i.d. random splits.
- Demonstrating **reliability diagnostics** (calibration, reliability diagrams, risk–coverage).
- Showing how **uncertainty** supports **selective prediction** (abstention/triage).
- Demonstrating **Bayesian optimisation** for expensive simulators.
- Demonstrating **multiobjective optimisation** with Pareto fronts and hypervolume.

### Out-of-scope uses
- Any clinical, safety-critical, or operational decision-making without domain-specific validation.
- Claims about real telescope, instrument, or physical system performance.
- Use as a drop-in predictor for real observational pipelines without retraining and shift testing.

## 3. Data
### Data type
- **Synthetic** light-curve style time series for regression and classification.
- **Synthetic physics-inspired simulators** for single-objective BO and two-objective MOBO++.

### Key dataset artifacts (typical)
- `timeseries_preview.csv`, `lightcurves_preview.csv`, `labels_table.csv`
- `regression_metrics.csv`, `classification_metrics.csv`
- `group_split_metrics.csv`, `ood_metrics.csv`

### Data splits used
- **Random split:** conventional i.i.d. partitioning.
- **Group split:** holds out correlated groups to reduce leakage.
- **OOD split:** explicit distribution shift to mimic deployment drift.

## 4. Training and evaluation
### Training setup (time-series)
Models are trained on synthetic time-series derived features/targets, then evaluated under:
- Random split,
- Group split,
- OOD split.

### Evaluation metrics (time-series)
- Classification: AUC summary and reliability diagnostics.
- Regression: task-specific regression metrics.
- Reliability and decision diagnostics:
  - Reliability diagrams: `reliability_random_split.png`, `reliability_group_split.png`, `reliability_ood.png`
  - Risk–coverage curves: `risk_coverage_random.png`, `risk_coverage_group.png`, `risk_coverage_ood.png`
  - Uncertainty–error coupling: `uncertainty_gamma_std_vs_error.png`, `uncertainty_omega0_std_vs_error.png`

### Training setup (BO/MOBO)
- **Single-objective BO:** GP surrogate fit to observed evaluations, sequential acquisition via EI or UCB.
- **MOBO++:** two GP surrogates (performance and cost), batch selection using random scalarisation plus diversity.

### Evaluation metrics (BO/MOBO)
- BO: best-so-far curve, BO vs random, surrogate mean/uncertainty maps, acquisition map.
- MOBO++: Pareto front size, Pareto ranks, hypervolume trajectory, hypervolume contributions, epsilon-constraint curve.
- Optional robustness probe: noiseless re-evaluation under a shifted simulator regime.

## 5. Key quantitative results (example outputs)
The following are example values produced in a representative run (seeded, synthetic):
- **Single-objective BO:** best observed objective ≈ **2.1198** at **(x1, x2) ≈ (0.5748, −0.1164)**.
- **MOBO++:** final hypervolume ≈ **83.8520**, Pareto front size ≈ **15**.
- **OOD shift probe (MOBO++):** worst noiseless performance drop across selected Pareto points ≈ **−0.5002**.

Exact results depend on random seed and configuration.

## 6. Ethical considerations and risks
- This repository is designed for **education and prototyping** using synthetic data.
- Reliability diagnostics are included specifically to reduce the risk of overconfident deployment.
- Users should not interpret the outputs as evidence of real-system readiness.

## 7. Limitations
- Synthetic data and simulators cannot cover all real astrophysical or experimental failure modes.
- OOD regimes here are simulated; real-world shift can be more complex and non-stationary.
- Model families are intentionally lightweight to keep the proof-of-concept readable and runnable.

## 8. Recommendations
If adapting to real data:
1) Replace synthetic data with domain datasets and document provenance.
2) Preserve **group** and **OOD** evaluation.
3) Add calibration procedures (e.g., temperature scaling / isotonic regression) and re-check reliability.
4) Treat uncertainty as a decision tool, validate risk–coverage trade-offs under real shift.
5) For BO/MOBO, align simulator objective functions with domain constraints and measurement costs.

## 9. How to run
### Single-objective BO

python uh_bayesopt_physics_poc.py --outdir uh_bo_outputs --acq ei --budget 60 --seed 42

# Datasheet for Datasets, Reliability-Critical Data Science for Physics/Astronomy/Mathematics (PoC)

## A. Motivation
### A.1. Why were these datasets created?
These datasets were created to provide a reproducible, teaching-ready proof-of-concept for **reliability-critical data science** workflows in Physics, Astronomy, and Mathematics. The aim is to demonstrate how evaluation choices (random vs group vs out-of-distribution splits) affect reported performance, calibration, and uncertainty usefulness, and how sequential design methods (BO/MOBO) can optimise expensive experiments under budget constraints.

## B. Composition
### B.1. What do the datasets contain?
This repository contains **synthetic** datasets and outputs from synthetic simulators, designed to mimic:
1) **Light-curve style time-series** for regression/classification tasks.
2) **Physics-inspired black-box objectives** for Bayesian optimisation (single-objective) and multiobjective optimisation (performance vs cost).

### B.2. How many instances are there?
Counts depend on run configuration (seed, number of generated series, and budgets). Metrics files summarise the effective sample sizes used in each experiment.

### B.3. What data does each instance consist of?
- **Time-series tasks:** rows typically represent individual time series or extracted features derived from a time series, plus targets/labels.
- **Optimisation tasks:** each row represents a candidate design point `(x1, x2)` with associated objective values.

### B.4. What are the labels?
- **Classification:** categorical labels derived from synthetic generative parameters or regimes.
- **Regression:** continuous targets derived from synthetic physical parameters (e.g., inferred period-like quantities or latent parameters).

## C. Collection process
### C.1. How were the datasets generated?
All datasets are generated programmatically using seeded random number generators. Data generation includes:
- Parameterised synthetic time-series generation (light-curve style), including noise.
- Split regimes to mimic different generalisation settings:
  - **Random split** (i.i.d.-like),
  - **Group split** (reduces leakage across correlated samples),
  - **OOD split** (explicit distribution shift).
- Physics-inspired simulator objectives with:
  - multi-modality,
  - noise,
  - cost terms,
  - feasibility/constraint penalties,
  - optional regime shift via parameter drift.

### C.2. Over what timeframe were the datasets generated?
Generated on demand when the scripts are executed.

### C.3. Were any human subjects involved?
No.

### C.4. Were any sensitive data collected?
No.

## D. Preprocessing, cleaning, and labeling
### D.1. Is there preprocessing?
Yes, but it is deterministic and reproducible. Typical preprocessing includes:
- feature extraction or summarisation from time-series,
- standardisation where needed for modelling,
- grouping metadata construction for group splits,
- optional calibration/reliability post-processing for diagnostics.

### D.2. Were there any filtering steps?
Filtering may occur to ensure valid time series (e.g., non-empty, finite values) and to enforce feasible regions for simulator constraints (soft penalties).

### D.3. How were labels generated?
Labels are generated from the synthetic generative process (not from annotation).

## E. Uses
### E.1. Recommended uses
- Teaching and demonstration of:
  - evaluation protocol pitfalls,
  - reliability and calibration,
  - uncertainty-aware decision-making,
  - Bayesian optimisation and multiobjective optimisation.
- Benchmarking alternative split strategies and uncertainty estimators.
- Rapid prototyping of reliability pipelines before moving to real observational/experimental datasets.

### E.2. Non-recommended uses
- Any high-stakes decisions (clinical, safety, operational).
- Claims about real telescope instrumentation or physical system performance.
- Model selection for real deployments without retraining and robust domain validation.

## F. Distribution
### F.1. How are the datasets distributed?
As CSV tables and JSON metrics reports produced by scripts. Data are stored locally in `tables/` (or within the specified `--outdir/tables/`).

### F.2. Are there any export controls or restrictions?
None known, as all data are synthetic (confirm based on your institution’s policy if needed).

## G. Maintenance
### G.1. Who maintains the datasets?
Mark I.R. Petalcorin
https://github.com/mpetalcorin

### G.2. Will the datasets be updated?
Yes, potentially, to improve realism of synthetic shifts, extend diagnostics, and add additional modelling baselines.

## H. File inventory and schema (practical)
Below are the key dataset artifacts typically produced. Exact columns can vary slightly by configuration; use the preview CSVs and metrics summaries as the source of truth.

### H.1. Time-series related CSVs
- `timeseries_preview.csv`  
  **Purpose:** compact preview of generated time-series features/targets and identifiers.  
  **Typical columns:** `series_id`, `group_id`, feature columns, regression targets (e.g., `period`-like).

- `lightcurves_preview.csv`  
  **Purpose:** preview of raw or lightly processed light-curve style observations.  
  **Typical columns:** `series_id`, `t` (time), `flux` (or signal), optional `err` (noise).

- `labels_table.csv`  
  **Purpose:** mapping between `series_id` and classification labels and metadata.  
  **Typical columns:** `series_id`, `label`, `group_id`, regime flags (e.g., `is_ood`).

- `regression_metrics.csv`  
  **Purpose:** summary regression metrics by split and model.  
  **Typical columns:** `split`, `model`, regression metrics (e.g., MAE/RMSE/R2 depending on implementation).

- `classification_metrics.csv`  
  **Purpose:** summary classification metrics by split and model.  
  **Typical columns:** `split`, `model`, `auc`, accuracy-like metrics if included.

- `group_split_metrics.csv`  
  **Purpose:** metrics computed specifically under group-based validation.  
  **Typical columns:** mirrors the metrics schema with `split=group`.

- `ood_metrics.csv`  
  **Purpose:** metrics computed under out-of-distribution evaluation.  
  **Typical columns:** mirrors the metrics schema with `split=ood`.

### H.2. Single-objective BO CSV/JSON
- `bo_trace.csv`  
  **Purpose:** per-iteration log of Bayesian optimisation evaluations.  
  **Typical columns:** `iter`, `x1`, `x2`, `y`, `cost`, `phase`, optional `best_y_before`.

- `metrics_report.json`  
  **Purpose:** run configuration and headline outcomes, including optional shift check.  
  **Typical fields:** `seed`, `budget`, `best_y_observed`, `best_x_observed`, `gp_kernel`, `ood_shift_check`.

### H.3. MOBO / MOBO++ CSV/JSON
- `mobo_trace.csv` or `mobo_plus_trace.csv`  
  **Purpose:** per-evaluation log of MOBO iterations (often includes batch metadata).  
  **Typical columns:** `iter`, `x1`, `x2`, `f1_perf`, `f2_cost`, `phase`, `batch_id`, optional acquisition metadata.

- `pareto_front.csv` or `pareto_front_plus.csv`  
  **Purpose:** extracted Pareto-optimal set with ranks and contributions.  
  **Typical columns:** `index`, `x1`, `x2`, `f1_perf`, `f2_cost`, `pareto_rank`, `hv_contribution`.

- `hypervolume_trace.csv`  
  **Purpose:** hypervolume over evaluation count.  
  **Typical columns:** `iter`, `hypervolume`.

- `epsilon_constraint_report.csv`  
  **Purpose:** best-performance solution under cost ceilings (ε).  
  **Typical columns:** `epsilon_cost`, `best_perf`, `cost`, `index`.

- `metrics_report.json`  
  **Purpose:** run config, final hypervolume, Pareto size, optional OOD shift checks.  
  **Typical fields:** `hypervolume_final`, `n_pareto_points`, `hv_reference_point`, `ood_shift_check_top_pareto`.

## I. Known caveats
- Synthetic shifts are controlled and may not represent real-world non-stationarity.
- Metrics are sensitive to seed and parameter settings; always report configuration.
- Reliability claims must be tied to the split regime; random splits are not deployment guarantees.

## J. How to regenerate
### Single-objective BO
```bash
python uh_bayesopt_physics_poc.py --outdir uh_bo_outputs --seed 42 --budget 60 --acq ei
