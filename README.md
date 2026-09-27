# pyETL

A Python ETL pipeline that extracts data from a REST API, transforms it, and loads it into PostgreSQL. It is designed to run once a day on a server.

> 🚧 Work in progress: the pipeline is being built step by step.

## Requirements

- [uv](https://docs.astral.sh/uv/): manages Python, the virtual environment, and dependencies.
  You do **not** need to install Python yourself; uv downloads the right version automatically.
- Git

### Install uv

macOS / Linux:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows (PowerShell):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Check that it works:

```bash
uv --version
```

## Getting started

```bash
git clone https://github.com/anasbayu/pyETL.git
cd pyETL
uv run pyetl
```

On the first run, uv will:

1. Install the Python version listed in `.python-version`
2. Create a virtual environment in `.venv/`
3. Install the exact dependency versions from `uv.lock`
4. Run the `pyetl` command

## Usage

Run the pipeline:

```bash
uv run pyetl
```

or, equivalently, as a Python module:

```bash
uv run -m pyetl
```

## Project structure

```
pyETL/
├── pyproject.toml      # project metadata, dependencies, and the `pyetl` command
├── uv.lock             # exact pinned versions of every dependency (commit this)
├── .python-version     # Python version used by uv
└── src/
    └── pyetl/
        ├── __init__.py # marks the package
        └── __main__.py # entry point: main()
```

## Development

Add a dependency:

```bash
uv add <package>
```

Add a development-only tool (e.g. tests, linting):

```bash
uv add --dev <package>
```

Upgrade dependencies:

```bash
uv lock --upgrade
```

## Deployment (server)

On the server, install exactly what is in `uv.lock` and skip development tools:

```bash
uv sync --frozen --no-dev
uv run --frozen --no-dev pyetl
```

<!--
TODO: once the pipeline reads settings, add a "Configuration" section:
  1. Commit a `.env.example` with placeholder values
  2. Tell users: `cp .env.example .env` and fill in the API key + database URL
  3. Make sure `.env` is listed in `.gitignore`
-->
