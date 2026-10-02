# <Название проекта>

[English version](README.md)

Семестровая НИР при проекте mas-science. Репозиторий создан из [шаблона](https://github.com/AnatolyPershinov/nir-mas-template), который построен на [шаблоне лаборатории](https://github.com/Industrial-AI-Research-Lab/nir-project-template). Замените этот абзац описанием проекта: вопрос, данные, ожидаемый результат.

## Первый запуск после «Use this template»

Сделайте это один раз, в первую неделю. Раздел удалите первым же pull request.

1. Создайте репозиторий из шаблона в личном аккаунте: кнопка **Use this template**, имя `nir-<тема>`. Рекомендуем публичный: только там GitHub бесплатно обеспечивает защиту ветки `main` и автоматический запрос ревью.
2. Клонируйте с подмодулями: `git clone --recurse-submodules git@github.com:<вы>/<репозиторий>.git`. Если папка `.agents/overlay` пуста, выполните `git submodule update --init`.
3. Создайте ветку `chore/project-setup` и переименуйте пакет: `make rename NAME=<имя_пакета>`, затем `uv lock`.
4. Подготовьте окружение командами из раздела «Быстрый старт» и убедитесь, что `make check` проходит.
5. Дайте доступ руководителю: Settings → Collaborators → `AnatolyPershinov`, право Write. В `.github/CODEOWNERS` он уже записан.
6. Откройте первый pull request `chore: set up the project`: переименование пакета и описание проекта в этом README.

Как работать дальше: [правила работы с git и GitHub](docs/git-workflow.ru.md). Прочитайте их до первого коммита.

## Быстрый старт

```bash
cp .env.example .env          # заполните ключи; .env не попадает в репозиторий
uv sync                       # ставит пакет и инструменты разработки из uv.lock
uvx pre-commit install        # gitleaks, большие файлы, make check перед каждым коммитом
make check                    # ruff, mypy, pytest
make run                      # один эксперимент: configs/smoke.yaml -> запуск в MLflow
make mlflow                   # интерфейс MLflow над локальной базой mlflow.db
```

## Структура

```
src/<пакет>/         код, который импортируется и тестируется: config.py, pipeline.py, __main__.py
tests/               smoke-тест: пайплайн на крошечном входе
configs/             конфиги экспериментов (YAML)
notebooks/           исследовательский анализ; вывод ячеек можно оставить как отчёт о результате
docs/adr/            журнал решений, один файл на решение
docs/meetings/       записи встреч
docs/reading-log.md  журнал чтения статей
data/                не попадает в репозиторий; как получить данные, написано ниже
results/             таблицы и рисунки, экспортированные из кода
.github/             шаблон PR, форма issue для экспериментов, CODEOWNERS, CI
```

## Данные

Данные в репозиторий не кладутся, в том числе открытые бенчмарки. Где лежат данные и как их получить: <заполните>.

## Эксперименты

Каждый запуск записывается в MLflow (`MLFLOW_TRACKING_URI` в `.env`, по умолчанию локальная база `mlflow.db`). Строка результата: коммит, путь к конфигу, seed, id запуска, метрики.

| коммит | конфиг | seed | id запуска | mse |
|---|---|---|---|---|

## Проверки

`make check` запускается из трёх мест: pre-commit на вашей машине, CI на каждом PR, хук агента. Ветка `<тип>/<короткое-описание>`, заголовок PR `<тип>: ...`; типы: feat, fix, refactor, docs, test, chore, exp. Подробно: [правила работы с git и GitHub](docs/git-workflow.ru.md).

## LLM-ассистенты

Какими агентами вы пользуетесь и для чего: <заполните>. Инструкции для них: [AGENTS.md](AGENTS.md); общие правила лаборатории уже подключены как подмодуль `.agents/overlay` на теге v0.1.0 ([nir-agent-overlay](https://github.com/Industrial-AI-Research-Lab/nir-agent-overlay)); другую версию подключает `make overlay OVERLAY_VERSION=<тег>`. За код, написанный с агентом, отвечаете вы.

## Памятки

[Практические памятки](https://github.com/Industrial-AI-Research-Lab/project-implementation-manual/blob/feat/practice-guides/nir-requirements/recommendations/README.ru.md) из руководства лаборатории: научные статьи, репозиторий и код, трекинг задач, агентные артефакты.

## Лицензия

Шаблон распространяется по MIT. Лицензию своего кода выберите сами и при необходимости замените LICENSE.
