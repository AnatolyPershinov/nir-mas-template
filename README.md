# <Project name>

[Русская версия](README.ru.md)

Semester research project (NIR) around the mas-science project. The repository was created from a [template](https://github.com/AnatolyPershinov/nir-mas-template) built on the [lab template](https://github.com/Industrial-AI-Research-Lab/nir-project-template). Replace this paragraph with the purpose of the project: the question, the data, the expected result.

## First run after "Use this template"

Do this once, in the first week. Remove this section in your first pull request.

1. Create the repository from the template in your personal account: the **Use this template** button, name `nir-<topic>`. A public repository is recommended: only there GitHub enforces `main` protection and automatic review requests for free.
2. Clone with submodules: `git clone --recurse-submodules git@github.com:<you>/<repository>.git`. If `.agents/overlay` is empty, run `git submodule update --init`.
3. Create the branch `chore/project-setup` and rename the package: `make rename NAME=<your_package>`, then `uv lock`.
4. Set up the environment with the commands from "Quick start" and make sure `make check` passes.
5. Give the supervisor access: Settings → Collaborators → `AnatolyPershinov`, Write permission. He is already listed in `.github/CODEOWNERS`.
6. Open the first pull request `chore: set up the project`: the package rename and the project description in this README.

How to work from then on: [git and GitHub rules](docs/git-workflow.ru.md) (in Russian). Read them before the first commit.

## Quick start

```bash
cp .env.example .env          # fill in the keys; .env is ignored
uv sync                       # installs the package and the dev tools from uv.lock
uvx pre-commit install        # gitleaks, large files, make check before every commit
make check                    # ruff, mypy, pytest
make run                      # one experiment: configs/smoke.yaml -> an MLflow run
make mlflow                   # MLflow UI over the local mlflow.db
```

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

Data is not committed, open benchmarks included. Where the data lives and how to fetch it: <fill in>.

## Experiments

Every run is recorded in MLflow (`MLFLOW_TRACKING_URI` in `.env`, the local `mlflow.db` by default). A results row is commit, config path, seed, run id, metrics.

| commit | config | seed | run id | mse |
|---|---|---|---|---|

## Checks

`make check` runs from three places: pre-commit on your machine, CI on every PR, the agent hook. Branch `<type>/<short-description>`, PR title `<type>: ...`; the types are feat, fix, refactor, docs, test, chore, exp. Details: [git and GitHub rules](docs/git-workflow.ru.md).

## LLM assistants

Which agents you use and for what: <fill in>. Their instructions: [AGENTS.md](AGENTS.md); the shared lab rules are already connected as the submodule `.agents/overlay` pinned to v0.1.0 ([nir-agent-overlay](https://github.com/Industrial-AI-Research-Lab/nir-agent-overlay)); `make overlay OVERLAY_VERSION=<tag>` connects another version. You are responsible for code written with an agent.

## Guides

[Practice guides](https://github.com/Industrial-AI-Research-Lab/project-implementation-manual/blob/feat/practice-guides/nir-requirements/recommendations/README.md) of the lab manual: papers, repository and code, task tracking, agent artifacts.

## Licence

The template is MIT. Choose the licence of your own code and replace LICENSE if needed.
