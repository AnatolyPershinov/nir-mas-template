# NIR for the mas-science project

[Русская версия](README.ru.md)

Semester student research projects (NIR) for the mas-science project, started from the [lab template](https://github.com/Industrial-AI-Research-Lab/nir-project-template). Each one builds a standalone tool next to the project on adaptive assembly of a multi-agent text2app pipeline. Four topics:

- **1A** — structural complexity of a requirements specification as a predictor of generation cost and success;
- **1B** — underspecification of a requirements specification: a measure based on the spread of independent interpretations;
- **2.1** — acceptance tests from a textual task description;
- **2.6** — a checklist judge of requirements coverage (metric Q2).

## Quick start

```bash
cp .env.example .env          # fill in the keys; .env is ignored
uv sync                       # installs the package and the dev tools from uv.lock
uvx pre-commit install        # gitleaks, large files, make check before every commit
make check                    # ruff, mypy, pytest
make run                      # one experiment: configs/smoke.yaml -> an MLflow run
make mlflow                   # MLflow UI over the local mlflow.db
```

Clone with `--recurse-submodules`, otherwise `.agents/overlay` stays empty. The package is already renamed to `nir_mas_science`.

## Layout

```
src/<package>/       code that is imported and tested: config.py, pipeline.py, __main__.py
tests/               smoke test: the pipeline on a tiny input
configs/             experiment configs (YAML)
notebooks/           exploration; outputs may stay as a report of a result
docs/adr/            decision log, one file per decision
docs/meetings/       meeting records
docs/reading-log.md  papers read
data/                ignored; how to fetch the data is described below
results/             tables and figures exported from code
.github/             PR template, issue form for experiments, CODEOWNERS, CI
```

## Data

The projects use the open benchmarks WebGen-Bench and DevAI. The data is not committed: `data/` is ignored. Where to get it and with which command: <fill in>.

## Experiments

Every run is recorded in MLflow (`MLFLOW_TRACKING_URI` in `.env`, the local `mlflow.db` by default). A results row is commit, config path, seed, run id, metrics.

| commit | config | seed | run id | mse |
|---|---|---|---|---|

## Checks

`make check` runs from three places: pre-commit on your machine, CI on every PR, the agent hook. Branch `<type>/<short-description>`, PR title `<type>: ...`; the types are feat, fix, refactor, docs, test, chore, exp.

## LLM assistants

Pull requests are reviewed by the supervisor's AI assistant. Which agents the authors use and for what: <fill in>. Their instructions: [AGENTS.md](AGENTS.md); the shared lab rules are connected by `make overlay` as the submodule `.agents/overlay` ([nir-agent-overlay](https://github.com/Industrial-AI-Research-Lab/nir-agent-overlay), tag v0.1.0). The author is responsible for code written with an agent.

## Guides

[Practice guides](https://github.com/Industrial-AI-Research-Lab/project-implementation-manual/blob/master/nir-requirements/recommendations/README.md) of the lab manual: papers, repository and code, task tracking, agent artifacts.

## Licence

The template is MIT. Choose the licence of your own code and replace LICENSE if needed.
