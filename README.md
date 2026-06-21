# FinLedger Pro

**A dual-currency, local-first desktop finance & accounting system for Singapore × China startups.**

*SGD + CNY · Fully offline · Privacy-first · AI-assisted*

![Status](https://img.shields.io/badge/status-in%20development-orange)
![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows%20%7C%20Linux-blue)
![Electron](https://img.shields.io/badge/shell-Electron-47848F)
![React](https://img.shields.io/badge/frontend-React%20%2B%20Tailwind-61DAFB)
![FastAPI](https://img.shields.io/badge/backend-Python%20FastAPI-009688)
![AI](https://img.shields.io/badge/AI-Ollama%20%2B%20LangGraph-000000)
![License](https://img.shields.io/badge/license-MIT-green)

---

## Table of Contents

- [Project Positioning](#project-positioning)
- [Why FinLedger Pro](#why-finledger-pro)
- [Design Principles](#design-principles)
- [Scope: What It Is / What It Is Not](#scope-what-it-is--what-it-is-not)
- [Key Features](#key-features)
- [Technical Architecture](#technical-architecture)
- [AI Workflow (LangGraph)](#ai-workflow-langgraph)
- [The Six Accounting Modules](#the-six-accounting-modules)
- [Single-Entry vs Double-Entry Bookkeeping](#single-entry-vs-double-entry-bookkeeping)
- [Dual-Currency & Dual-Market Support](#dual-currency--dual-market-support)
- [The Three Financial Statements](#the-three-financial-statements)
- [Development Roadmap](#development-roadmap)
- [Final Deliverables](#final-deliverables)
- [Companion Finance Learning Path](#companion-finance-learning-path)
- [Project Conventions](#project-conventions)
- [Planned Repository Structure](#planned-repository-structure)
- [What Makes It Production-Grade](#what-makes-it-production-grade)
- [Financial Correctness Rules (Non-Negotiable)](#financial-correctness-rules-non-negotiable)
- [Production Readiness Checklist](#production-readiness-checklist)
- [Project Status](#project-status)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Project Positioning

**FinLedger Pro** is a localized desktop finance and accounting management system built for founders who run startups and micro/small businesses across **two markets at once: Singapore and China**. It treats *financial management and accounting record-keeping* as its core, with *AI analysis and tax-knowledge lookup* as supporting capabilities. Every piece of data lives on the user's own machine — there is no cloud dependency, no server to operate, and no account to sign up for.

The name encodes the positioning:

| Part | Meaning |
|------|---------|
| **Fin** | Finance — cash flow, budgeting, financial health |
| **Ledger** | The accounting core — the book of record, journals, and statements |
| **Pro** | A professional-grade tool, not a toy or a spreadsheet replacement |

At its heart, FinLedger Pro answers a single question for its user: *"As a founder operating in both Singapore and China, can I keep correct books, see my real cash position, and understand my numbers — entirely on my own machine, without handing my financial data to anyone?"*

It is deliberately a **single-user, locally-run, fully-offline** tool. The target user is not an accounting firm or a finance team — it is **the founder personally**, someone who needs to own their numbers, stay compliant-aware across two jurisdictions, and make decisions without depending on cloud SaaS or external bookkeepers for day-to-day visibility.

---

## Why FinLedger Pro

Founders operating simultaneously in Singapore and China face a specific set of problems that mainstream accounting tools do not solve well:

- **Two currencies, one reality.** Revenue and costs arrive in both SGD and CNY, but the founder still needs *one* consolidated view of the business. Most tools assume a single home currency.
- **Two regulatory worlds.** Payroll, social contributions, and tax references differ sharply between Singapore (CPF, GST, 17% corporate tax) and China (五险一金 / "Five Insurances and One Fund", VAT, 25% corporate tax). Generic software ignores this split.
- **Data sovereignty.** Financial data is among the most sensitive data a company holds. Cloud bookkeeping means trusting a third party with it. FinLedger Pro keeps everything in a local SQLite file the user fully controls.
- **Cost and lock-in.** Cloud accounting subscriptions accumulate cost and lock founders into a vendor. A local, offline, one-machine tool has no recurring cost and no lock-in.
- **Understanding, not just recording.** A ledger that only stores numbers is half a tool. FinLedger Pro layers a local AI analysis engine on top so the founder gets cash-flow trends, anomaly detection, forecasts, and plain-language advice — bilingual, and computed entirely on-device.

---

## Design Principles

1. **Local-first.** All computation and storage happen on the user's machine. The application is fully usable with the network cable unplugged.
2. **Privacy by architecture.** Financial data never leaves the device. The AI model (Ollama / Qwen2.5) runs locally, so even AI analysis does not transmit data anywhere.
3. **Offline by default, online by exception.** The only optional online touchpoints are exchange-rate refresh and tax-knowledge-base updates — both cached locally and never required for core use.
4. **Accounting-correct.** The engine supports proper double-entry bookkeeping (every debit has a matching credit) so the three financial statements can be generated to standard.
5. **Dual-market native.** Singapore and China differences are first-class concepts in the data model, not afterthoughts.
6. **AI as an assistant, not an authority.** AI provides analysis, forecasts, and tax *references with citations* — it never files taxes or makes binding financial decisions.
7. **Educational by design.** The project is built as a structured learning vehicle: the software is constructed in phases that map directly onto a finance & accounting curriculum (see [Companion Finance Learning Path](#companion-finance-learning-path)).

---

## Scope: What It Is / What It Is Not

| ✅ FinLedger Pro **is** | ❌ FinLedger Pro **is not** |
|------------------------|----------------------------|
| A local desktop finance & accounting tool | A cloud / SaaS accounting service |
| Single-user, owned by the founder | A multi-user team or accounting-firm platform |
| A tool that *records, reports, and analyzes* finances | A **tax-filing** or statutory-submission system |
| A provider of tax-knowledge *reference lookups* (with citations) | A source of legally binding tax or audit advice |
| Fully offline-capable | Dependent on internet connectivity |
| Bilingual (English / Chinese) for SG + CN | Single-market or single-language |

> **Important boundary:** Tax features are **reference only**. The system helps the founder *look up and understand* relevant tax provisions via a local RAG knowledge base — it does **not** perform tax declaration, filing, or submission. Always consult a qualified accountant or compliance advisor for official filings.

---

## Key Features

- **Dual bookkeeping modes** — switch freely between single-entry (cash-flow style) and double-entry (debit/credit, GAAP-aligned) bookkeeping.
- **Dual-currency input & consolidation** — record in SGD or CNY; the system auto-converts to a unified reference currency (SGD) for summary reporting.
- **Six accounting modules** — covering the full operational chain from revenue recognition to fixed-asset depreciation (see below).
- **Automatic three-statement generation** — P&L, Balance Sheet, and Cash Flow Statement generated from underlying vouchers.
- **Excel & PDF export** — share statements with accountants or compliance advisors.
- **Local AI analysis engine** — cash-flow trends, anomaly detection, 30/60/90-day forecasts, and bilingual advice, all computed on-device.
- **Tax-knowledge RAG (reference)** — vector search over imported tax PDFs with cited, source-backed answers.
- **Offline exchange rates** — SGD ↔ CNY conversion with local caching and optional auto-refresh when online.
- **Bilingual UI** — switch the interface between English and Chinese.

---

## Technical Architecture

FinLedger Pro uses a three-layer architecture — **desktop shell + local backend + local AI model** — in which all computation and data remain on the user's machine.

> 📐 For the system-design rationale — the **"narrow-waist" extensible architecture** that lets the system grow to meet a small company's full needs without rewriting the core — see [docs/architecture.md](docs/architecture.md).

| Layer | Technology | Notes |
|-------|------------|-------|
| **Desktop shell** | Electron | Cross-platform: macOS / Windows / Linux |
| **Frontend** | React + Tailwind CSS | Single/double-entry toggle, SGD/CNY dual-currency display |
| **Backend service** | Python FastAPI | Launched and embedded by Electron as a local HTTP service |
| **AI analysis engine** | LangChain + LangGraph | Multi-node workflow: analyze → alert → advise |
| **Local LLM** | Ollama (Qwen2.5) | Fully offline, bilingual (EN/ZH), data never leaves the machine |
| **Financial database** | SQLite | Local file, no server required |
| **Tax knowledge base** | ChromaDB + RAG | Vector retrieval, PDF import, reference lookup only |
| **Currency conversion** | ExchangeRate API (cached) | Real-time SGD ↔ CNY with local cache |

```
┌─────────────────────────────────────────────────────────┐
│                    Electron Desktop Shell                 │
│  ┌─────────────────────────┐   ┌──────────────────────┐  │
│  │   React + Tailwind UI    │   │   Embedded Backend    │  │
│  │  (single/double entry,   │◄──┤   Python FastAPI       │  │
│  │   SGD/CNY, EN/ZH)        │   │   (local HTTP)        │  │
│  └─────────────────────────┘   └──────────┬───────────┘  │
│                                            │              │
│        ┌───────────────────┬───────────────┼───────────┐ │
│        ▼                   ▼               ▼           ▼ │
│   ┌─────────┐      ┌──────────────┐  ┌──────────┐ ┌─────┐│
│   │ SQLite  │      │ LangGraph AI │  │ ChromaDB │ │ FX  ││
│   │ (books) │      │  + Ollama    │  │  (tax    │ │cache││
│   │         │      │  (Qwen2.5)   │  │   RAG)   │ │     ││
│   └─────────┘      └──────────────┘  └──────────┘ └─────┘│
└─────────────────────────────────────────────────────────┘
        All data and computation stay on the local machine
```

---

## AI Workflow (LangGraph)

When the user triggers an analysis, the request flows through a sequence of LangGraph nodes:

1. **Router node** — classify the request type (financial analysis / profit interpretation / cash alert / tax reference).
2. **Data-collection node** — read recent financial data from SQLite.
3. **Analysis node** — compute cash-flow trends and identify anomalous spending.
4. **Risk-detection node** — check balance alerts and overdue receivables.
5. **Forecast node** — project cash flow for the next 30 / 60 / 90 days.
6. **Advice-generation node** — local Ollama inference produces bilingual (EN/ZH) recommendations.
7. **Tax-RAG node (supporting)** — vector-retrieve relevant tax provisions and return cited references.

---

## The Six Accounting Modules

The system covers the full operational accounting chain and supports free switching between single-entry and double-entry bookkeeping.

| Module | Capabilities | Region |
|--------|--------------|--------|
| **Revenue Recognition** | Contract management, deferred/installment amortization, three-state tracking (invoiced / received / recognized) | SG + CN |
| **Cost Accounting** | Direct/indirect cost classification, project allocation, automatic gross-margin calculation | SG + CN |
| **Receivables & Payables (AR/AP)** | Invoice tracking, aging analysis (30/60/90 days), overdue alerts, payment schedules | SG + CN |
| **Payroll & Compensation** | Singapore CPF / China Five-Insurances-One-Fund, automatic payslip generation | SG / CN |
| **Fixed-Asset Depreciation** | Straight-line / double-declining-balance methods, monthly auto-accrual, asset register | SG + CN |
| **Profit Analysis** | Three-tier analysis (gross / operating / net profit), 12-month trend, AI interpretation | SG + CN |

---

## Single-Entry vs Double-Entry Bookkeeping

**Single-entry** — like a bank statement: records date, amount, category, and running balance. Best for fast entry of day-to-day income and expenses; simple and intuitive.

**Double-entry** — follows the debit/credit principle (*every debit must have a matching credit; debits must equal credits*). Strictly aligned with accounting standards and supports automatic generation of the three financial statements. Best when the books must be reported externally or audited.

The user can switch between the two modes freely as their needs evolve.

---

## Dual-Currency & Dual-Market Support

### Currency Handling

- Record transactions in **SGD** or **CNY**.
- All transactions are automatically converted to a **unified reference currency (SGD)** for consolidated reporting.
- Exchange-rate data is **cached locally** for offline use and refreshed automatically when online.
- Statements can be displayed in three modes: **SGD only**, **CNY only**, or **side-by-side dual-currency comparison**.

### Singapore vs China Business Differences

| Item | Singapore | China |
|------|-----------|-------|
| **Primary currency** | SGD | CNY |
| **Payroll & social security** | CPF (Employee 20% + Employer 17%) | Five-Insurances-One-Fund (rates vary by locality) |
| **Tax reference** | GST 9%, Corporate Income Tax 17% | VAT 6% / 13%, Corporate Income Tax 25% |
| **Financial year** | Apr–Mar or Jan–Dec (selectable) | Jan–Dec |
| **Report language** | Bilingual (EN/ZH) | Chinese |

> Tax rates above are reference figures for understanding and analysis — not official filing guidance.

### Payroll & Social Contributions (the hardest module)

Payroll is the most complex of the six modules because **statutory social-contribution rules differ by jurisdiction, change every year, and depend on more than a flat percentage of salary**. The system therefore models both schemes with **configurable rates** (stored in editable configuration, not hard-coded), so the user can update them when policy changes without a new release.

**Singapore — CPF (Central Provident Fund / 中央公积金):**
A mandatory retirement, housing, and healthcare savings scheme. Both employer and employee contribute a percentage of monthly wages (commonly ~17% employer + ~20% employee for younger workers), split across Ordinary, Special, and MediSave accounts. Rates **step down by age band**, are capped by a **monthly wage ceiling**, and apply only to **citizens and permanent residents** — not foreign work-pass holders.

**China — Five Insurances and One Fund (五险一金):**
Five social insurances — pension (养老), medical (医疗), unemployment (失业), work-injury (工伤, employer only), maternity (生育, employer only) — plus the Housing Provident Fund (住房公积金). Both sides contribute, each at its own rate. Critically, **the rates and the contribution base (缴费基数, with a local floor and ceiling) are set per city/province** and revised periodically, so the same salary produces different deductions in Beijing vs Shenzhen.

**Employment relationship types (`employment_type`):**

Before any contribution math runs, payroll must know *what kind of working relationship* a person has — it changes wage calculation, which contributions apply, the tax treatment, and whether a written contract is legally required. The module models three types:

| Type | 🇨🇳 China | 🇸🇬 Singapore |
|------|-----------|---------------|
| **Full-time employee** (labor relationship) | Full 五险一金; written labor contract required within 1 month (missing it triggers a double-wage penalty) | CPF for citizens / PRs; written Key Employment Terms (KET) within 14 days |
| **Part-time / non-full-time** (labor relationship) | 非全日制: ≤ 4 h/day & ≤ 24 h/week, hourly pay, employer typically owes **work-injury insurance only**, verbal agreement allowed, terminable anytime with no severance | Part-time (< 35 h/week): hourly / pro-rated wages and benefits, CPF still applies to citizens / PRs |
| **Contractor / freelancer** (service relationship) | 劳务关系: service agreement, **no social insurance**, taxed as labor remuneration (劳务报酬), not salary | Independent contractor / self-employed: service agreement, **no CPF** (self-employed pays own MediSave) |

The `employment_type` field drives four downstream decisions:

1. **Wage calculation** — monthly salary vs hourly rate × hours worked.
2. **Which contributions apply** — full scheme / work-injury only / none.
3. **Tax treatment** — employment income vs labor-remuneration withholding.
4. **Contract requirement** — written contract / written terms / service agreement.

All rates and contribution bases stay in editable configuration so they can be updated per locality and year without a code change. *(Rules above are general reference, not legal advice — confirm with IRAS/MOM, the local 人社局, or a professional before acting.)*

**Why it is built last and split SG-first:** the rules are external, locale-specific, and frequently updated, making this the most error-prone module and the one most coupled to policy. Singapore CPF is implemented first; China's locale-dependent rules follow.

---

## The Three Financial Statements

From the entered vouchers and business data, the system automatically generates the three standard financial statements, with monthly / quarterly / annual rollups:

- **Profit & Loss (P&L)** — Revenue → Gross Profit → Operating Profit → Net Profit, with automatic gross-margin and net-margin calculation.
- **Balance Sheet** — Assets (current + non-current) = Liabilities + Owner's Equity, generated automatically from voucher data.
- **Cash Flow Statement** — Operating / Investing / Financing cash flows, supporting both the direct and indirect methods.

All statements export to **Excel (.xlsx)** and **PDF** for sharing with accountants or compliance advisors.

---

## Development Roadmap

The project is built as a sequence of phases over roughly seven weeks. **Phase 0 builds a thin end-to-end "walking skeleton" first**, then later phases widen it. Tests, linting, and CI are set up in Phase 0 and maintained continuously — not bolted on at the end. Treat this as the path to a usable **v0.1**, with full payroll and the AI engine as stretch goals rather than guaranteed completions.

| Phase | Timeline | Deliverable |
|-------|----------|-------------|
| **Phase 0** | Week 1 (first half) | 🆕 Walking skeleton: record one transaction end-to-end (Electron → FastAPI → SQLite → React list) + test / lint / CI scaffolding |
| **Phase 1** | Weeks 1–2 | Accounting core: **chart of accounts**, vouchers/journal, double-entry posting with **balance validation**, **trial balance**, single/double-entry switching, `Decimal` money — with unit & property tests written alongside. Plus a minimal **automatic backup**. |
| **Phase 2** | Week 3 | Backend APIs for the six modules, ordered by value: revenue / cost / AR / AP first, then assets, then payroll (**Singapore CPF first, China later**) |
| **Phase 3** | Week 4 | React frontend build-out + Electron desktop packaging |
| **Phase 4** | Week 5 | Automatic three-statement generation (built on the trial balance) + Excel/PDF export |
| **Phase 5** | Week 6 | Ollama integration + LangGraph AI analysis engine (minimal, supporting) |
| **Phase 6** | Week 7 | Tax RAG knowledge base (reference) + full end-to-end testing, code-signing & packaging |

---

## Final Deliverables

On completion, the project ships as directly installable desktop packages:

- `FinLedger-Pro-Mac.dmg` — macOS installer
- `FinLedger-Pro-Win.exe` — Windows installer
- `FinLedger-Pro-Linux.AppImage` — Linux installer

**Post-install experience:**

- Double-click the icon to launch; the FastAPI service and Ollama model start automatically in the background.
- No server configuration and no internet connection required — works out of the box.
- All financial data is stored in a local SQLite file the user can back up freely.
- The tax knowledge base can be updated with a built-in one-click tool (requires internet).
- The interface supports switching between Chinese and English.

---

## Companion Finance Learning Path

This project is built as a **teaching project**: the author writes the code themselves, paced alongside a structured finance & accounting curriculum. Each week of learning maps directly onto the software module being built, so theory is applied immediately.

| Week | Learning Topic | Corresponding Software Module |
|------|----------------|-------------------------------|
| **Week 1** | The five accounting elements + debit/credit rules | Ledger module (single/double-entry toggle) |
| **Week 2** | Revenue recognition + cost accounting | Revenue module + Cost module |
| **Week 3** | Receivables/payables + aging analysis | AR/AP module |
| **Week 4** | Payroll calculation (SG + CN) | Payroll module |
| **Week 5** | Fixed-asset depreciation methods | Fixed-asset module |
| **Week 6** | Comprehensive three-statement exercises | Statement-generation module |

---

## Project Conventions

This repository follows a **teaching-mode** workflow:

- **All documentation is written in English.**
- **All code comments are written in English.**
- **Teaching and discussion happen bilingually (Chinese + English).**
- **The author writes all the code personally** — this repo is a learning vehicle, not a code-generation target. Assistance is for guidance, review, and explanation, not for writing the implementation.

---

## Planned Repository Structure

> Indicative layout — to be created as the project is built phase by phase.

```
FinLedgerPro/
├── electron/            # Electron main process, app lifecycle, backend bootstrap
├── frontend/            # React + Tailwind UI
│   ├── src/
│   └── ...
├── backend/             # Python FastAPI service
│   ├── accounting/      # Core engine: single/double-entry, vouchers, journals
│   ├── modules/         # Revenue, Cost, AR/AP, Payroll, Assets, Profit
│   ├── statements/      # P&L, Balance Sheet, Cash Flow generators + exporters
│   ├── ai/              # LangChain / LangGraph workflow + Ollama integration
│   ├── tax_rag/         # ChromaDB + RAG tax-knowledge lookup
│   └── db/              # SQLite schema, migrations, data access
├── data/                # Local SQLite file, FX cache, imported tax PDFs (gitignored)
├── docs/                # English documentation
├── LICENSE
└── README.md
```

---

## What Makes It Production-Grade

"Production-grade" does not mean *more features* — it means **people can trust real money and real business decisions to the software**. For a local-first accounting tool, that trust rests on six pillars. This section is the engineering standard the project is built to.

### 1. Correctness & Financial Integrity

The accounting engine is the part where a bug is unacceptable, because it silently produces wrong numbers.

- **Money is `Decimal`, never `float`.** Floating-point cannot represent `0.1` exactly; using it for currency produces rounding errors that break reconciliation. All monetary values use fixed-precision decimal types end to end (Python `Decimal`, `NUMERIC` in SQLite, string-based transport in JSON).
- **Double-entry must balance.** Every posted journal entry is validated so total debits equal total credits before it is committed. An unbalanced entry is rejected, not stored.
- **Vouchers are immutable + audit trail.** Posted entries are never edited or deleted in place; corrections are made via reversing entries. Every record carries `created_at`, `created_by`, and a reason, forming an audit log.
- **Deterministic rounding.** Currency conversion and tax math use explicit, documented rounding rules (e.g. banker's rounding, 2 decimal places) so results are reproducible.
- **ACID transactions.** Multi-step postings run inside a single database transaction — they either all succeed or all roll back.

### 2. Testing & Quality Gates

- **Unit tests** for the accounting engine, currency conversion, depreciation, and payroll math — high coverage on the financial core specifically.
- **Property-based tests** for invariants (e.g. "debits always equal credits", "balance sheet always balances").
- **Integration tests** for the FastAPI endpoints against a real temporary SQLite database.
- **End-to-end tests** for the Electron app (e.g. Playwright) covering the critical user flows.
- **Golden-file tests** for generated statements (P&L / Balance Sheet / Cash Flow) and Excel/PDF exports.
- **Static quality:** linting (`ruff` / `eslint`), formatting (`black` / `prettier`), type checking (`mypy` strict, TypeScript `strict: true`), enforced via pre-commit hooks and CI.

### 3. Security & Privacy

- **Encryption at rest.** The SQLite database is encrypted (e.g. SQLCipher) and unlocked by a user passphrase — losing the laptop must not mean losing the books.
- **Localhost-only backend.** The embedded FastAPI service binds to `127.0.0.1` only and is protected by a per-session token shared with the Electron process, so no other local process can read the financial API.
- **Strict input validation.** All API input is validated with Pydantic schemas; nothing untrusted reaches the database.
- **Signed installers.** macOS builds are code-signed and notarized; Windows builds are code-signed — otherwise the OS warns users the app is untrusted.
- **Dependency hygiene.** Dependencies are pinned (lockfiles) and scanned for known vulnerabilities in CI.
- **No telemetry by default.** Consistent with the privacy-first positioning, the app ships with no analytics; any future telemetry is strictly opt-in and local-only.

### 4. Reliability & Data Safety

Because all data lives in one local SQLite file, **data loss is the single biggest risk** — this gets first-class treatment.

- **Schema migrations.** Database schema changes are versioned and applied via a migration tool (e.g. Alembic) so upgrading the app never corrupts existing books.
- **Automatic backups.** The app takes timestamped local backups on a schedule and before every migration, with one-click restore.
- **Integrity checks.** On startup the app runs `PRAGMA integrity_check` and verifies the books still balance; problems are surfaced, not hidden.
- **Crash recovery.** Write-ahead logging (WAL) and atomic writes ensure an interrupted save never leaves a half-written ledger.
- **Graceful degradation.** If the AI model or exchange-rate refresh is unavailable, core accounting keeps working — these are non-critical dependencies.

### 5. Build, Release & Updates

- **CI/CD pipeline.** Every change runs tests, linting, and type checks; tagged releases build and package the three installers automatically (GitHub Actions or equivalent).
- **Semantic versioning + changelog.** Releases follow `MAJOR.MINOR.PATCH` with a maintained `CHANGELOG.md`.
- **Auto-update.** The desktop app supports safe in-place updates (e.g. `electron-updater`) so users get fixes without manual reinstalls.
- **Reproducible builds.** Locked dependency versions and pinned toolchains so a given tag always builds the same artifact.

### 6. Observability & Supportability

- **Structured logging.** The backend logs in structured form (JSON), with levels, to local rotating log files — never logging sensitive financial values.
- **User-visible error reporting.** Errors surface as clear, actionable messages (bilingual), not silent failures or raw stack traces.
- **Diagnostics export.** A built-in "export diagnostics" tool bundles logs and environment info (no financial data) to make support possible for a local app.

---

## Financial Correctness Rules (Non-Negotiable)

These are domain rules that distinguish a real accounting system from a generic CRUD app. They are listed separately because **violating any of them produces wrong financial statements**:

1. **Use `Decimal` for every monetary amount.** Never `float`, never binary floating point — anywhere, including intermediate calculations.
2. **Debits = Credits, always.** Reject any journal entry that does not balance.
3. **Assets = Liabilities + Equity, always.** The balance sheet must reconcile; if it does not, that is a bug, not a rounding artifact.
4. **Post, don't mutate.** Correct mistakes with reversing entries; never silently edit a posted voucher.
5. **One source of truth for FX.** Store the exchange rate used *on each transaction*, so historical reports don't change when today's rate changes.
6. **Round once, explicitly, and at the boundary.** Define where rounding happens and to how many decimals; never let it happen implicitly mid-calculation.
7. **Separate "recognized" from "received".** Revenue recognition and cash receipt are different events — model them separately (accrual vs cash).

---

## Production Readiness Checklist

A pragmatic "definition of done" for shipping FinLedger Pro as a real product. Items are aspirational targets for the build, not yet implemented.

| Category | Item | Target |
|----------|------|--------|
| **Correctness** | `Decimal` money everywhere; balanced-entry validation | ☐ |
| **Correctness** | Property tests for accounting invariants | ☐ |
| **Testing** | Engine unit coverage ≥ 90% | ☐ |
| **Testing** | E2E tests for critical flows | ☐ |
| **Security** | Encrypted SQLite (passphrase) | ☐ |
| **Security** | Localhost-only API + session token | ☐ |
| **Security** | Signed & notarized installers | ☐ |
| **Reliability** | Versioned DB migrations | ☐ |
| **Reliability** | Automatic backups + one-click restore | ☐ |
| **Reliability** | Startup integrity + balance check | ☐ |
| **Release** | CI runs tests/lint/types on every change | ☐ |
| **Release** | Auto-update for the desktop app | ☐ |
| **Release** | SemVer + maintained changelog | ☐ |
| **Observability** | Structured local logs (no sensitive data) | ☐ |
| **Docs** | API docs (OpenAPI), ADRs, runbook | ☐ |

---

## Project Status

🚧 **In development — at Phase 0, building not yet started.** Where the project stands today (June 2026):

**Decided / done**
- ✅ Positioning, scope, and architecture defined (this document).
- ✅ Tech stack chosen (Electron + React/Tailwind + FastAPI + Ollama/LangGraph + SQLite + ChromaDB).
- ✅ Licensed under **MIT**.
- ✅ Engineering standards and financial-correctness rules agreed (see above).
- ✅ Roadmap refined to start with a walking skeleton and test-as-you-go.

**Not started yet**
- ⬜ No application code written — the repository currently holds only documentation and the license.
- ⬜ Phase 0 walking skeleton is the immediate next step.

**Next step:** Phase 0 — scaffold the repo and get a single transaction flowing end-to-end (Electron → FastAPI → SQLite → React), with `Decimal` money and the test/CI harness in place from day one.

This is a **teaching project**: the author writes all code personally (see [Project Conventions](#project-conventions)). The production-readiness items above are targets to build toward, not yet implemented.

---

## License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for the full text.

MIT is a short, permissive license: anyone may use, copy, modify, merge, publish, distribute, sublicense, and sell the software — including in **closed-source and commercial** products — as long as they keep the original copyright and license notice. The software is provided "as is", without warranty. This keeps adoption frictionless and leaves the door open to a future commercial edition.

## Acknowledgements

- Project summary and positioning authored with assistance from Claude (Anthropic), June 2026.

---

*FinLedger Pro — Own your finances, own your data, own your decisions.*
