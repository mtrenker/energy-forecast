# Data and evaluation

## Candidate and provenance

- Dataset: [A real-world energy management data set from a smart company building](https://doi.org/10.5061/dryad.73n5tb363).
- Paper: [Scientific Data](https://www.nature.com/articles/s41597-025-05186-3).
- Location: Honda R&D Europe, Offenbach am Main, Germany.
- Period: 2018–2023, hourly aggregates available.
- Dryad metadata specifies CC0-1.0 for the dataset; the paper has its own licence.
- Reduced archive approximately 320 MB; full archive approximately 103 GB. Start with reduced data and issue logs, not the full archive.
- Sources verified during planning; no data downloaded into this repository yet. Record the exact version, files and checksums when importing.

The dataset includes PV and CHP generation: grid imports are not the same as total facility consumption. Select the target after reading column descriptions and sign conventions. Do not silently substitute net imports.

Readings were cleaned and corrected. Audit the relevant issue logs; distinguish measured, inferred and gap-filled data. Some historical corrections use hindsight. Document this limitation; a replay on corrected final data is not an operational as-of archive.

## Forecast contract to confirm after audit

- Proposed issue time: 18:00 Europe/Berlin on the preceding day.
- Predict the next local calendar day's hourly intervals; DST days have 23 or 25 hours, not always 24.
- Store UTC instants, derive local calendar features explicitly.
- Define interval-start/interval-end semantics and observation latency before feature generation.
- Features may depend on target calendar information but observed measurements must be available by issue time. A target-relative lag is valid only if its source interval was already available.
- Begin with calendar features, seasonal lags and trailing statistics. No weather required for the first demand model.
- Future observed weather is not a legitimate day-ahead input. Adding weather requires suitable historical forecast vintages or an explicitly labelled hindsight experiment.

## Evaluation

Compare same-hour-last-week and recent matching weekday/hour averages, with missing baseline inputs handled explicitly. Use chronological development splits and a final untouched period. Fit preprocessing on training data only.

Begin with MAE and errors by weekday/weekend, season and hour. Report peak magnitude/timing errors if peak planning becomes a product claim. If using MASE, define its seasonal denominator from training data; it is not simply a test-set error ratio. Avoid MAPE for near-zero readings.

Exclude invalid/imputed target intervals from scoring and report the excluded fraction. Check whether repaired historical inputs introduce hindsight. Changing a hypothetical feature is not evidence of a causal intervention.

The model need not beat the baseline for the experiment to be valuable. Report the result, do not cherry-pick a building or period after seeing final-test performance.

## Stop or reconsider

Reconsider if the target's meaning cannot be resolved, usable measured coverage cannot support the split, or correction flags cannot support an honest evaluation. Missingness alone is not a universal fixed-percentage rejection rule: assess its timing and impact.

Alternative: German national load from SMARD. That permits ongoing data but changes the product to a national aggregate with reporting delays/revisions. Residual load and renewable-generation forecasting still depend on weather; they do not remove that difficulty.
