# Working agreement

Read README.md and docs/data-and-evaluation.md first.

## Learning and delivery

This repository exists to learn classical ML, feature engineering, data processing and application delivery through a real-data experiment.

- Optimize for the maintainer's understanding, not agent output volume. Explain unfamiliar ML concepts and consequential alternatives before implementing them. Do not build on code or results the maintainer cannot explain.
- Work in increments suitable for 1–2-hour learning sessions. Keep one issue in progress; a pull request may span sessions. End unfinished sessions with a concise continuation note.
- After the initial bootstrap, track work in issues with a bounded outcome, verification steps and a stopping point. Implement on a dedicated branch/worktree and deliver a small linked PR.
- Record real decisions, experiments, failures and review findings. Do not fabricate retrospective issues or activity.
- Done means working, checked and understood by the maintainer. Report skipped or failed checks. Agents may assist with implementation and review; the maintainer owns decisions and explicitly authorizes merges.
- Keep public documentation focused on learning goals, project behavior and evidence.

## Engineering boundaries

- Build the smallest useful increment. The current milestone is a real-data audit and baseline backtest, not a complete platform.
- Preserve the distinction between planned, implemented, locally tested and actually deployed.
- Use the agreed Kotlin/Spring Boot + Python/Databricks architecture when the data milestone justifies application implementation. Do not create placeholder services to tick technology boxes.
- Do not claim energy savings or forecast skill without evidence.
- Never use future observations as forecast inputs. Track issue time and target time separately. Test cutoff boundaries, including Europe/Berlin DST.
- Fit learned transforms only on training data. Keep a final untouched evaluation period. Do not score imputed targets as real observations.
- All raw/derived datasets, credentials, workspace configuration and model artifacts stay out of Git.
- No public publishing, cloud provisioning, paid compute, cluster mutation or remote database writes without explicit authorization and effective-target verification.
- The eventual hosting goal is the maintainer's existing Kubernetes cluster, using the infrastructure repository's Helm/Argo CD workflow. This is planned, not deployed. Read that repository's current instructions before proposing integration; do not copy private topology, credentials or operational configuration here. Kubernetes hosting does not establish Azure usage.
- Keep commands and explanations usable without an agent. Record consequential decisions in concise repository documentation.
