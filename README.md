# When Does Machine Learning Help? Predicting DB and DC Pension Benefits

ECON 81230 Machine Learning for Economists, Fall 2026 — research project (Track A: Application)
Hyeonji Jang

## Question
Does the predictive gain of machine learning over linear benchmarks differ between
defined benefit (DB) and defined contribution (DC) pension benefits? The project builds on
Kwon and Maliar (2026) and Bajari et al. (2015). See `proposal/` for details.

## Data
RAND HRS Longitudinal File 1992–2022 (V1), supplemented by the RAND HRS Fat Files.
Both are available after free registration at https://hrs.isr.umich.edu.
**Data files are not included in this repository** (HRS conditions of use do not allow redistribution).
Place the data in a local `data/` folder (ignored by git) or set `PATH` in the first cell of each notebook.

## Repository structure
```
proposal/   project proposal (PDF and source)
code/       analysis notebooks, run in numerical order
```

## How to run
1. `code/01_sample_construction.ipynb` — builds the analysis sample (incl. job-history verification of the pre-claiming job) the outcome and the attrition table
2. `code/02_features.ipynb` — extracts and preprocesses the common and extended feature sets (CPI-U, 2022 dollars; previous-wave fill)
3. `code/03_descriptives.ipynb` — descriptive statistics by plan type, before and after the previous-wave fill (CSV and LaTeX)

Decisions and robustness candidates are logged in `notes/analysis_decisions.md`.

Random seeds are fixed in each notebook.
