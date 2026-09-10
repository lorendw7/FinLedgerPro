# Development Setup

[English](development-setup.md) | [简体中文](development-setup.zh-CN.md)

FinLedger Pro currently contains its product design and development baseline; application scaffolding begins in M1. This guide pins the tools already available on the maintainer's Windows machine so future work is reproducible without an unnecessary global upgrade.

## Pinned baseline

| Tool | Project requirement | Purpose |
|---|---:|---|
| Node.js | `24.14.0` (`>=24.14.0 <25`) | Electron and React toolchain |
| pnpm | `11.9.0` (`>=11.9.0 <12`) | JavaScript workspace and lockfile |
| CPython | `3.13` (`>=3.13,<3.14`) | FastAPI and accounting domain code |
| uv | `0.11.7` or compatible | Python interpreter, virtual environment, and lockfile |
| Git | `2.53.0` or compatible | Source control |

Docker, Ollama, ChromaDB, and SQLCipher are not required for the M1 scaffold. They will be introduced only when a milestone needs them.

## Verify the host tools

From PowerShell in the repository root:

```powershell
node --version
pnpm --version
uv --version
git --version
```

Expected major versions are Node 24, pnpm 11, and Python 3.13. The exact project choices are recorded in `.node-version`, `.python-version`, `package.json`, and `pyproject.toml`.

## Create the local environment

```powershell
pnpm install --frozen-lockfile
uv sync --frozen
Copy-Item .env.example .env
```

`uv sync` creates a repository-local `.venv` using CPython 3.13. Run Python commands through `uv run`; do not activate Anaconda or add its packages to this project environment.

```powershell
uv run python --version
uv run python -c "import sqlite3; print(sqlite3.sqlite_version)"
```

The `.env`, `.venv`, `node_modules`, local databases, exports, and backups are ignored by Git.

## Workspace layout

The JavaScript workspace is ready for the planned `electron/` and `frontend/` packages. Python remains a non-published root project until the M1 backend package is scaffolded. Empty package directories are intentionally not created yet.

The root `package.json` contains `"private": true` only to prevent accidental publication to the npm registry. It does **not** make the repository proprietary or change the MIT License and the project's [Open-Source and Free-Forever Commitment](../OPEN_SOURCE_COMMITMENT.md).

## Secrets and financial data

Use `.env.example` only as a safe template. Never commit real bank credentials, API tokens, account identifiers, ledger databases, invoices, exports, or backups. Read-only banking credentials should eventually be stored in the operating-system credential store or another local secret manager, not in this repository or a company extension repository.

## Updating the baseline

Change pinned versions deliberately and in one pull request. Update both setup guides, regenerate `pnpm-lock.yaml` and `uv.lock`, run frozen installs, and record the change in both changelogs.
