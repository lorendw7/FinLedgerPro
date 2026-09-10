# 开发环境配置

[English](development-setup.md) | [简体中文](development-setup.zh-CN.md)

FinLedger Pro 目前包含产品设计和开发基线，M1 才开始搭建应用代码。本指南按照维护者 Windows 电脑上已经可用的工具锁定版本，避免为了开始开发而进行不必要的全局升级。

## 锁定的环境基线

| 工具 | 项目要求 | 用途 |
|---|---:|---|
| Node.js | `24.14.0`（`>=24.14.0 <25`） | Electron 和 React 工具链 |
| pnpm | `11.9.0`（`>=11.9.0 <12`） | JavaScript 工作区和锁文件 |
| CPython | `3.13`（`>=3.13,<3.14`） | FastAPI 和会计领域代码 |
| uv | `0.11.7` 或兼容版本 | Python 解释器、虚拟环境和锁文件 |
| Git | `2.53.0` 或兼容版本 | 版本控制 |

M1 脚手架暂时不需要 Docker、Ollama、ChromaDB 或 SQLCipher；等对应里程碑真正需要时再引入。

## 检查本机工具

在仓库根目录打开 PowerShell：

```powershell
node --version
pnpm --version
uv --version
git --version
```

预期主版本为 Node 24、pnpm 11 和 Python 3.13。项目的准确选择记录在 `.node-version`、`.python-version`、`package.json` 和 `pyproject.toml` 中。

## 创建本地环境

```powershell
pnpm install --frozen-lockfile
uv sync --frozen
Copy-Item .env.example .env
```

`uv sync` 会使用 CPython 3.13 创建仓库内的 `.venv`。请通过 `uv run` 执行 Python 命令，不要为本项目启用 Anaconda，也不要把 Anaconda 中的包混入项目环境。

```powershell
uv run python --version
uv run python -c "import sqlite3; print(sqlite3.sqlite_version)"
```

`.env`、`.venv`、`node_modules`、本地数据库、导出和备份均已被 Git 忽略。

## 工作区结构

JavaScript 工作区已经为计划中的 `electron/` 和 `frontend/` 包做好准备。在 M1 后端包建立前，Python 根项目不作为可发布软件包。当前不会为了占位而创建空目录。

根目录 `package.json` 中的 `"private": true` 只用于防止误发到 npm 软件包仓库，不表示仓库闭源，也不会改变 MIT 许可证或项目的[永久开源与免费承诺](../OPEN_SOURCE_COMMITMENT.zh-CN.md)。

## 秘密信息与财务数据

`.env.example` 只能作为安全模板。不得提交真实银行凭据、API Token、账户标识、账簿数据库、发票、导出或备份。未来只读银行接口的凭据应保存在操作系统凭据库或其他本地秘密管理器中，不应写入本仓库或公司扩展仓库。

## 更新环境基线

工具版本应有计划地统一升级。升级时同时更新两种语言的环境指南，重新生成 `pnpm-lock.yaml` 和 `uv.lock`，执行冻结安装验证，并在中英文变更日志中记录。
