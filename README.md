# Energy forecast

A learning project for classical machine learning, feature engineering and application delivery, using historical energy data from a German facility.

**Status:** repository and Python/notebook environment bootstrapped. No dataset imported, model trained, application implemented, or cloud resources deployed yet.

## Product

At a fixed issue time, predict the next local calendar day's electricity consumption. The intended application is a historical forecast explorer: select a forecast date, compare predicted demand with actual measurements and simple baselines, and inspect where forecasts succeed or fail. This is a historical demonstrator, not a live meter feed or proven energy-saving system.

The learning goal is to understand the complete path from raw observations through trustworthy evaluation to a deployed application. Each increment should be runnable, checked and explainable by its maintainer.

Initial data candidate: Honda R&D Europe's Offenbach facility, 2018–2023. It includes consumption, PV generation, CHP, heating/cooling and weather. Confirm the target meter and quality before committing to a model.

## Intended stack

| Technology | Intended responsibility | Current state |
|---|---|---|
| Python / scikit-learn | Feature engineering, classical ML, temporal backtesting | Environment configured |
| Jupyter | Explainable data audit and experiments | First audit notebook |
| Databricks / SQL / Delta / MLflow | Data processing, experiment tracking, reproducible jobs | Workspace capabilities to be verified |
| Kotlin / Spring Boot | Serve stored forecasts and evaluation results | Planned |
| PostgreSQL | Application-side forecast and run storage | Planned |
| Docker / GitHub Actions | Reproducible builds and CI | Planned |
| Kubernetes / Argo CD | Host the demonstrator on an existing Kubernetes cluster through GitOps | Planned, no cluster access performed |
| Azure | Verify and document actual Azure usage if provisioned | Not provisioned or evidenced |
| React | Historical forecast explorer after the data milestone | Later |

Kotlin is the JVM language choice. Databricks is the intended data platform; the first experiments run locally. Technology choices support learning through working increments, not placeholder services.

## Start locally

Requires Python 3.12 and [uv](https://docs.astral.sh/uv/).

```sh
uv sync --extra notebooks
uv run jupyter lab notebooks/01_data_audit.ipynb
```

Set `ENERGY_DATA_CSV` to one extracted hourly CSV or gzip CSV before starting Jupyter. The notebook stops with an actionable message if none is selected; it does not download data or silently substitute synthetic readings.

The notebook is an initial inspection tool, not a completed data-quality assessment. The dataset's column semantics and correction logs must be reviewed alongside it.

## First milestone

1. Read the dataset documentation and correction logs; choose one electricity target with explicit unit and sign conventions.
2. Inspect coverage, missing/corrected periods, timestamps and regime changes.
3. Document the chronological development split and reserve an untouched final evaluation period.
4. Evaluate seasonal-naive baselines on real, valid development observations.
5. Explain the audit and baseline results, including exclusions, limitations and failures.

The first milestone is a reproducible real-data audit and baseline backtest, not a trained model or hosted service. Rejecting the dataset with documented evidence is a valid audit outcome. After this milestone, train one simple classical model and compare it with the baselines before building the application.

Do this before adding a backend or deployment scaffolding. No chatbot, vector database, scenario sliders, equipment control, or hyperparameter search in this increment.

See [data and evaluation constraints](docs/data-and-evaluation.md).

## Learning workflow

Work in sessions of about 1–2 hours, with one question or small outcome per session. Use an initial two-week checkpoint to review data suitability and progress, not as a delivery deadline.

- Track each bounded investigation or implementation in a GitHub issue with an outcome, verification steps and a stopping point.
- Work on a branch and submit a small pull request linked to the issue. A PR can span several sessions.
- Record consequential decisions, actual checks and negative results. End unfinished sessions with a short continuation note in the issue.
- Discuss unfamiliar ML concepts before implementing them. Agent-assisted code must remain understandable and reproducible by the maintainer.
- Merge only when the change works, relevant checks pass and the maintainer understands it. Agent review supports, but does not replace, maintainer review.

The initial commit records the repository bootstrap. Subsequent work uses issues and pull requests; no retrospective process history is invented.

## Later deployment

After the data and application increments, package the demonstrator in containers and host it on the maintainer's existing Kubernetes cluster. Follow the infrastructure repository's Helm and Argo CD GitOps workflow, with reviewed rollout, rollback and operational checks. Keep cluster-specific configuration and secrets outside this repository.

This is a future learning goal, not a deployment claim. No infrastructure changes or cluster access have been performed for this project. The existing hosting target is separate from any future Azure learning; Kubernetes hosting alone is not evidence of Azure usage.

## Boundaries

Keep credentials, meter data, model artifacts and workspace exports out of Git. Verify cloud identity, cost limits and deployment targets before remote writes.
