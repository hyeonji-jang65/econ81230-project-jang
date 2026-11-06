# Analysis decisions and robustness candidates

Running log of decisions for the sample, features and preprocessing.
Items marked **[pending]** are not yet implemented in code.

## 1. Analysis sample (implemented in `code/01_sample_construction.ipynb`)

- Born 1931–1953, HRS / War Babies / Early Baby Boomer cohorts (`hacohort` 3–5)
- Pension onset (t0) observed after a non-receipt wave
- Pension received in two consecutive waves (t0, t0+1)
- Exactly one pension in receipt at t0
- At least one working wave before t0; the last one is t1
- Not self-employed at t1; pension on the t1 job
- Job-history verification
  - interviewed in every wave between t1 and t0
  - observed not working in every wave between t1 and t0
  - tenure on the t1 job positive and at most (age − 14)
- DB: single DB plan on the t1 job; DC: all plans on the t1 job are DC (balances summed)
- Positive pension income at t0 and t0+1
- Outcome within the 1st–99th percentile, separately for DB and DC
- Count before cohort restriction and trimming: 887 DB / 406 DC (rerun for the final count)

## 2. Decisions

| # | Topic | Decision |
|---|---|---|
| 1 | Cohort | Keep only HRS, War Babies, Early Baby Boomers (`hacohort` 3–5) |
| 2 | t1–t0 gap | Keep gaps > 3 waves (early retirement with deferred DB benefit is common) |
| 3 | Outcome | Log real **monthly** pension, mean of t0 and t0+1; CPI-U, 2022 dollars; income deflated with CPI of (interview year − 1) |
| 4 | RAND-imputed outcome | Keep in main sample |
| 5 | Outliers | Drop top and bottom 1% of the outcome, separately for DB and DC |
| 6 | Lump sums / non-annuitized DC | Out of scope (interest is post-retirement cash flow); mention in text only |
| 7 | No pension / no pension info codes | Recode to 0; such cases are not in the sample by construction |
| 8 | Missing values | Structural codes recoded (`.u` → 0 for spouse variables, `.z`/`.s` → 0 for pension variables, `.w` → 0 hours); then the respondent's own value one wave earlier (max. 1 wave); remaining missing → median + missing indicator inside CV folds **[pending: modeling stage]** |
| 9 | Occupation / industry | Current-job codes at t1, version fallback `jcocc → jcoccb → jcoccc` (same for industry); each version mapped to groups from its own labels: occupation 4 groups, industry 5 groups |
| 10 | Categorical variables | One-hot encoding; merge rare categories; aim for ≤ 4–5 categories |
| 11 | Weights | Unweighted |
| 12 | Descriptive tables | Mean with (SD) below, missing-rate column next to the mean; two tables, before and after previous-wave fill |

## 3. Robustness check candidates

- [ ] Restrict t1–t0 gap to ≤ 3 waves
- [ ] Outcome from t0+1 only (first-wave income may cover a partial year of receipt)
- [ ] Exclude respondents whose outcome is RAND-imputed
- [ ] Multiple DB plans allowed (DB)
- [ ] Single DC plan only (DC)
- [ ] Exclude the respondent flagged by the new-employer tenure check
- [ ] Sample without job-history verification
- [ ] Exclude SSDI / disability recipients (reference code drops them)
