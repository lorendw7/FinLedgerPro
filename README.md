# FinLedger Pro

**Free, open-source, local-first finance software — personal bookkeeping for everyone, full business accounting when you need it.**

*Basic (personal) + Pro (business) · SGD + CNY · Fully offline · Privacy-first · AI-assisted · MIT*

![Status](https://img.shields.io/badge/status-in%20development-orange)
![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows%20%7C%20Linux-blue)
![Electron](https://img.shields.io/badge/shell-Electron-47848F)
![React](https://img.shields.io/badge/frontend-React%20%2B%20Tailwind-61DAFB)
![FastAPI](https://img.shields.io/badge/backend-Python%20FastAPI-009688)
![AI](https://img.shields.io/badge/AI-Ollama%20%2B%20LangGraph-000000)
![License](https://img.shields.io/badge/license-MIT-green)
![Price](https://img.shields.io/badge/price-free%20forever-brightgreen)

---

## Table of Contents

- [Project Positioning](#project-positioning)
- [Feature Tiers: Basic & Pro](#feature-tiers-basic--pro)
- [Everything Is Free and Open Source](#everything-is-free-and-open-source)
- [Why FinLedger Pro](#why-finledger-pro)
- [Design Principles](#design-principles)
- [Scope: What It Is / What It Is Not](#scope-what-it-is--what-it-is-not)
- [Technical Architecture](#technical-architecture)
- [Basic Tier — Personal Ledger](#basic-tier--personal-ledger)
- [Pro Tier — Business Accounting](#pro-tier--business-accounting)
- [Single-Entry vs Double-Entry Bookkeeping](#single-entry-vs-double-entry-bookkeeping)
- [Dual-Currency & Dual-Market Support](#dual-currency--dual-market-support)
- [The Three Financial Statements](#the-three-financial-statements)
- [AI Workflow (LangGraph)](#ai-workflow-langgraph)
- [Development Roadmap](#development-roadmap)
- [Final Deliverables](#final-deliverables)
- [Companion Finance Learning Path](#companion-finance-learning-path)
- [Project Conventions](#project-conventions)
- [Planned Repository Structure](#planned-repository-structure)
- [What Makes It Production-Grade](#what-makes-it-production-grade)
- [Financial Correctness Rules (Non-Negotiable)](#financial-correctness-rules-non-negotiable)
- [Production Readiness Checklist](#production-readiness-checklist)
- [Project Status](#project-status)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## Project Positioning

**FinLedger Pro** is a **free and open-source, local-first desktop finance application** organised into two feature tiers:

- **Basic — Personal bookkeeping.** Track where your money actually goes: accounts, categories, budgets, and spending analysis. Simple enough that no accounting knowledge is required. This is the default experience.
- **Pro — Business accounting.** Full double-entry accounting for a startup or micro-business: chart of accounts, six operational modules, three financial statements, dual-market payroll (Singapore + China), AI analysis, and tax-knowledge lookup. Switched on when you need it.

Every piece of data lives on the user's own machine — no cloud dependency, no server to operate, no account to sign up for. **Both tiers are completely free and MIT-licensed** (see [Everything Is Free and Open Source](#everything-is-free-and-open-source)).

### What the name means

| Part | Meaning |
|------|---------|
| **Fin** | Finance — cash flow, budgeting, financial health |
| **Ledger** | The accounting core — the book of record, journals, and statements |
| **Pro** | Professional-grade engineering, for everyone — *not* a paid edition |

> **A note on naming.** "Pro" appears in two places and means two related things: the **product name** signals professional-grade quality applied to the whole application, while the **Pro tier** names the advanced business-accounting feature set. Neither implies a price — the entire product is free.

### Who it is for

- **Anyone who wants to control personal spending** — the Basic tier stands entirely on its own. You never have to see a debit or a credit.
- **Founders running a startup across Singapore and China** — the Pro tier adds proper books, dual-currency consolidation, and dual-jurisdiction payroll, on the same private local machine.

At its heart the application answers two questions, one per tier: *"Where is my money going, and can I spend less?"* and *"Are my company's books correct, and is it actually making money?"*

---

## Feature Tiers: Basic & Pro

| | 🟢 **Basic — Personal** | 🔵 **Pro — Business** |
|---|---|---|
| **Availability** | Always on, default experience | Opt-in toggle in settings |
| **Price** | Free | Free |
| **Accounting knowledge needed** | None | Debits and credits |
| **Book type** | `PERSONAL` | `BUSINESS` (one per entity) |
| **Basis** | Cash basis (收付实现制) | Accrual basis (权责发生制) |
| **Method** | Single-entry (cash-flow style) | Double-entry (借 = 贷) |
| **Accounts** | Cash, bank, e-wallet, credit card | Full chart of accounts |
| **Records** | Transactions: income / expense / transfer | Vouchers and journal entries |
| **Categories** | Hierarchical income/expense categories | Chart-of-accounts hierarchy |
| **Budgeting** | Monthly budgets + alerts, need/want tagging | Project cost budgets |
| **Analysis** | Spending breakdown, savings rate, recurring-charge detection | Trial balance, gross/operating/net profit, aging |
| **Business modules** | — | Revenue, Cost, AR/AP, Payroll, Fixed Assets, Profit |
| **Payroll** | — | CPF (SG) · 五险一金 (CN) · piece-rate 劳务 |
| **Statements** | Monthly income/expense summary | P&L, Balance Sheet, Cash Flow |
| **Multi-currency** | Record in SGD or CNY with a manual rate | Auto FX rates, per-transaction rate snapshot, consolidation |
| **Multi-entity** | Single personal book | Multiple entities (SG + CN) + consolidated view |
| **AI analysis** | Spending insights | Cash-flow forecasting, anomaly detection, advice |
| **Tax knowledge (reference)** | — | RAG lookup with citations |
| **Export** | CSV | Excel (.xlsx) + PDF |

### Where the tier boundary sits — and why

The line between Basic and Pro is exactly the line between **single-entry cash-basis** and **double-entry accrual** bookkeeping. That is a genuine conceptual step: below it, anyone can record a coffee purchase; above it, the user must understand that every debit needs a matching credit.

The boundary therefore exists for **progressive disclosure**, not monetisation. A person who only wants to stop overspending should never be confronted with a chart of accounts. A founder who needs auditable books should not be limited to a spending tracker. One application serves both by revealing complexity only when it is asked for.

**Basic is fully useful standalone.** It is not a demo, a trial, or a crippled version of Pro. It is a complete personal-finance tool that happens to share a kernel with a business accounting system.

---

## Everything Is Free and Open Source

**There is no paid tier, no licence key, no subscription, no feature paywall, and no telemetry.**

- The complete source code — Basic *and* Pro — is published under the **[MIT License](LICENSE)**.
- "Pro" denotes an **advanced feature set**, not a commercial edition. Enabling it is a settings toggle, not a purchase.
- This is **not** an open-core model: nothing is withheld in a proprietary edition.
- Anyone may use, modify, redistribute, or build commercial products on top of the code, provided the copyright notice is retained.

---

## Why FinLedger Pro

**For personal use:**

- **Spending outruns awareness.** Money leaves through dozens of small, invisible channels — most people cannot say where it went. Recording it is the only way to see it.
- **Privacy.** Personal spending is intimate data. Mainstream budgeting apps upload it, sell insights from it, or lose it in a breach. This one keeps it in a file on your own disk.
- **No subscription.** Budgeting software charging a monthly fee to help you spend less is a contradiction. This is free forever.

**For business use:**

- **Two currencies, one reality.** Revenue and costs arrive in both SGD and CNY, but the founder still needs *one* consolidated view. Most tools assume a single home currency.
- **Two regulatory worlds.** Payroll and tax references differ sharply between Singapore (CPF, GST, 17% corporate tax) and China (五险一金, VAT, 25% corporate tax). Generic software ignores this split.
- **Data sovereignty.** Financial data is among the most sensitive data a company holds; cloud bookkeeping means trusting a third party with it.
- **Understanding, not just recording.** A local AI engine turns the ledger into cash-flow trends, anomaly detection, forecasts, and plain-language bilingual advice — computed entirely on-device.

---

## Design Principles

1. **Local-first.** All computation and storage happen on the user's machine. Fully usable with the network cable unplugged.
2. **Privacy by architecture.** Financial data never leaves the device. The AI model (Ollama / Qwen2.5) runs locally, so even AI analysis transmits nothing.
3. **Free and open, entirely.** Every feature in every tier is MIT-licensed and free. No paywalls, no open-core withholding.
4. **Progressive disclosure.** Complexity appears only when asked for. Basic hides everything a personal user does not need; Pro reveals it on request.
5. **Offline by default, online by exception.** The only optional online touchpoints are exchange-rate refresh and tax-knowledge updates — both cached and never required.
6. **Accounting-correct.** The Pro kernel implements proper double-entry bookkeeping so the three statements can be generated to standard.
7. **Dual-market native.** Singapore and China differences are first-class concepts in the data model, not afterthoughts.
8. **AI as an assistant, not an authority.** AI provides analysis, forecasts, and *cited* tax references — it never files taxes or makes binding decisions.
9. **Educational by design.** Built as a structured learning vehicle: phases map onto a finance & accounting curriculum (see [Companion Finance Learning Path](#companion-finance-learning-path)).

---

## Scope: What It Is / What It Is Not

| ✅ FinLedger Pro **is** | ❌ FinLedger Pro **is not** |
|------------------------|----------------------------|
| A free, MIT-licensed, local desktop finance tool | A cloud / SaaS service, or a paid product |
| Two tiers in one app: personal (Basic) + business (Pro) | An open-core product with a proprietary paid edition |
| Single-user, owned by the person running it | A multi-user team or accounting-firm platform |
| A tool that *records, reports, and analyzes* finances | A **tax-filing** or statutory-submission system |
| A provider of tax-knowledge *reference lookups* (with citations) | A source of legally binding tax or audit advice |
| Fully offline-capable | Dependent on internet connectivity |
| Bilingual (English / Chinese) for SG + CN | Single-market or single-language |

> **Important boundary:** Tax features are **reference only**. The system helps the user *look up and understand* relevant tax provisions via a local RAG knowledge base — it does **not** perform tax declaration, filing, or submission. Always consult a qualified accountant or compliance advisor for official filings.

---

## Technical Architecture

FinLedger Pro uses a three-layer runtime architecture — **desktop shell + local backend + local AI model** — in which all computation and data remain on the user's machine.

> 📐 For the system-design rationale — the **"narrow-waist" architecture** and how the Basic and Pro tiers layer onto one shared kernel — see [docs/architecture.md](docs/architecture.md).

| Layer | Technology | Notes |
|-------|------------|-------|
| **Desktop shell** | Electron | Cross-platform: macOS / Windows / Linux |
| **Frontend** | React + Tailwind CSS | Tier-aware UI, SGD/CNY display, EN/ZH switch |
| **Backend service** | Python FastAPI | Launched and embedded by Electron as a local HTTP service |
| **AI analysis engine** | LangChain + LangGraph | Multi-node workflow: analyze → alert → advise |
| **Local LLM** | Ollama (Qwen2.5) | Fully offline, bilingual, data never leaves the machine |
| **Database** | SQLite | Local file, no server required |
| **Tax knowledge base** | ChromaDB + RAG | Vector retrieval, PDF import, reference lookup only |
| **Currency conversion** | ExchangeRate API (cached) | SGD ↔ CNY with local cache |

**Tier layering.** Both tiers run on one shared kernel — books, accounts, `Decimal` money, transactions, audit trail, and persistence. `personal/` and `pro/` are two feature layers above it. Enabling Pro mounts additional modules and routes; it does not fork the data model or launch a second application.

```
┌─────────────────────────────────────────────────────────┐
│                    Electron Desktop Shell                 │
│  ┌─────────────────────────┐   ┌──────────────────────┐  │
│  │   React + Tailwind UI    │   │   Embedded Backend    │  │
│  │  Basic view / Pro view   │◄──┤   Python FastAPI       │  │
│  │  SGD/CNY · EN/ZH         │   │   (localhost only)    │  │
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

## Basic Tier — Personal Ledger

**Built first.** The Basic tier is the default experience and the first thing implemented: the owner's day-to-day money needs visibility now, and it doubles as the walking skeleton that proves the kernel (accounts, `Decimal` money, transactions, reports) end to end.

### Strict separation: personal ≠ business

Under the **entity assumption**, a person and their company are two distinct accounting entities whose books must never merge. The system enforces this with separate books:

| | `book_type = PERSONAL` (Basic) | `book_type = BUSINESS` (Pro) |
|---|---|---|
| **Basis** | Cash basis — recorded when money actually moves | Accrual basis |
| **Method** | Single-entry | Double-entry |
| **Question it answers** | Where is my money going? Can I spend less? | Is the company profitable? |
| **Consolidation** | **Never consolidated with business books** | Consolidated across SG + CN entities |

Money crossing the boundary is modelled explicitly, never as an expense in the wrong book:

| Situation | Correct treatment |
|-----------|-------------------|
| Company account pays a personal expense | Dr **Other receivable — shareholder** (a loan to the owner), not a company expense |
| Owner's own money pays a company cost | Cr **Other payable — shareholder** (company owes the owner) |
| Owner takes money out of the company | **Owner's draw / dividend / salary**, with an explicit nature |

### Three transaction kinds — `TRANSFER` is not spending

The single most common personal-bookkeeping error is counting a *movement* of money as *spending*. The model therefore has three distinct kinds:

- **`INCOME`** — money enters personal net worth.
- **`EXPENSE`** — money leaves personal net worth. **Only this counts toward spending totals and budgets.**
- **`TRANSFER`** — money moves between the user's own accounts (bank → e-wallet, or a **credit-card repayment**). Net worth is unchanged, so it is **excluded from all spending statistics**.

Credit cards are modelled as **liability accounts**: swiping the card is an expense *and* increases the liability; repaying the card is a **transfer**. Treating both as expenses would double-count every card purchase.

### Spending-control features

Recording alone does not reduce spending — it only creates visibility. These features supply the actual levers:

- **Fast capture** — the primary screen is "add a transaction", with smart defaults (today's date, last-used account, most-recent categories). *Entry speed is the single biggest factor in whether bookkeeping is sustained; anything over ~10 seconds gets abandoned.*
- **Hierarchical categories** — e.g. Food → Takeaway, Transport → Ride-hailing.
- **Need vs Want tagging** — every expense is flagged `NEED` or `WANT`, enabling 50/30/20-style analysis (50% needs, 30% wants, 20% savings).
- **Monthly budgets with alerts** — per category and overall, with a warning threshold (e.g. 80% consumed).
- **Recurring-subscription detection** — surfaces silent auto-renewing charges (memberships, cloud storage, software), the most commonly overlooked drain.
- **Where-did-it-go analysis** — top categories, largest single expenses, month-over-month comparison, and **savings rate** = (income − expense) / income.

### Data model (blueprint)

```
book                    # 账套 — personal and business are separate books
  id, name, book_type = PERSONAL | BUSINESS, base_currency

account                 # 资金账户
  id, book_id, name
  account_kind = CASH | BANK | EWALLET | CREDIT_CARD    # card = liability
  currency, opening_balance (Decimal), is_active

category                # 收支分类, hierarchical
  id, book_id, name, kind = INCOME | EXPENSE, parent_id

transaction             # 流水 — the heart of the Basic tier
  id, book_id, txn_date
  kind = INCOME | EXPENSE | TRANSFER
  account_id, to_account_id (TRANSFER only)
  category_id, amount (Decimal), currency, fx_rate (Decimal)
  need_or_want = NEED | WANT (EXPENSE only)
  merchant, note, tags, attachment, is_recurring
  created_at

budget                  # 预算
  id, book_id, period (YYYY-MM), category_id (null = overall)
  limit_amount (Decimal), alert_threshold
```

**Balances are derived, never stored.** An account's balance is computed as `opening_balance + Σ inflows − Σ outflows`. A stored, mutable balance field inevitably drifts out of sync with the transactions and becomes untrustworthy — the transaction history is the single source of truth.

---

## Pro Tier — Business Accounting

Enabling Pro mode adds a full double-entry accounting system on top of the same kernel. It is aimed at a founder running a startup or micro-business, particularly across Singapore and China.

### The accounting core

- **Chart of accounts** — the account tree every entry posts against.
- **Vouchers & journal** — the immutable book of record.
- **Double-entry posting** — validates `debits == credits` before commit; unbalanced entries are rejected.
- **Trial balance** — the bridge from journal to the three financial statements.

### The six business modules

The Pro tier covers the full operational accounting chain.

| Module | Capabilities | Region |
|--------|--------------|--------|
| **Revenue Recognition** | Contract management, deferred/installment amortization, three-state tracking (invoiced / received / recognized) | SG + CN |
| **Cost Accounting** | Direct/indirect cost classification, project allocation, automatic gross-margin calculation | SG + CN |
| **Receivables & Payables (AR/AP)** | Invoice tracking, aging analysis (30/60/90 days), overdue alerts, payment schedules | SG + CN |
| **Payroll & Compensation** | Singapore CPF / China 五险一金 / piece-rate 劳务, automatic payslip generation | SG / CN |
| **Fixed-Asset Depreciation** | Straight-line / double-declining-balance methods, monthly auto-accrual, asset register | SG + CN |
| **Profit Analysis** | Three-tier analysis (gross / operating / net profit), 12-month trend, AI interpretation | SG + CN |

---

## Single-Entry vs Double-Entry Bookkeeping

**Single-entry** (Basic) — like a bank statement: records date, amount, category, and running balance. Best for fast entry of day-to-day income and expenses; simple and intuitive.

**Double-entry** (Pro) — follows the debit/credit principle (*every debit must have a matching credit; debits must equal credits*). Strictly aligned with accounting standards and supports automatic generation of the three financial statements. Best when the books must be reported externally or audited.

Turning on Pro mode does not migrate or convert the personal book — the two remain separate sets of books, as the entity assumption requires.

---

## Dual-Currency & Dual-Market Support

### Currency Handling

- Record transactions in **SGD** or **CNY**. Basic supports a manual rate; Pro adds automatic rates and consolidation.
- Pro converts all transactions to a **unified reference currency (SGD)** for consolidated reporting.
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

Payroll is the most complex Pro module because **statutory social-contribution rules differ by jurisdiction, change every year, and depend on more than a flat percentage of salary**. The system therefore models both schemes with **configurable rates** (stored in editable configuration, not hard-coded), so the user can update them when policy changes without a new release.

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

1. **Wage calculation** — monthly salary vs hourly rate × hours worked vs **piece-rate (计件)**: `Σ(accepted_qty × unit_price)`.
2. **Which contributions apply** — full scheme / work-injury only / none.
3. **Tax treatment** — employment income vs labor-remuneration withholding.
4. **Contract requirement** — written contract / written terms / service agreement.

All rates and contribution bases stay in editable configuration so they can be updated per locality and year without a code change. *(Rules above are general reference, not legal advice — confirm with IRAS/MOM, the local 人社局, or a professional before acting.)*

**Why it is built last and split SG-first:** the rules are external, locale-specific, and frequently updated, making this the most error-prone module and the one most coupled to policy. Singapore CPF is implemented first; China's locale-dependent rules follow. A worked example of the piece-rate 劳务 flow is in [docs/architecture.md](docs/architecture.md#8-worked-example-data-annotation-piece-rate-flow).

---

## The Three Financial Statements

*(Pro tier.)* From the entered vouchers and business data, the system automatically generates the three standard financial statements, with monthly / quarterly / annual rollups:

- **Profit & Loss (P&L)** — Revenue → Gross Profit → Operating Profit → Net Profit, with automatic gross-margin and net-margin calculation.
- **Balance Sheet** — Assets (current + non-current) = Liabilities + Owner's Equity, generated automatically from voucher data.
- **Cash Flow Statement** — Operating / Investing / Financing cash flows, supporting both the direct and indirect methods.

All statements export to **Excel (.xlsx)** and **PDF** for sharing with accountants or compliance advisors.

---

## AI Workflow (LangGraph)

When the user triggers an analysis, the request flows through a sequence of LangGraph nodes:

1. **Router node** — classify the request type (spending analysis / profit interpretation / cash alert / tax reference).
2. **Data-collection node** — read recent financial data from SQLite.
3. **Analysis node** — compute spending or cash-flow trends and identify anomalies.
4. **Risk-detection node** — check budget overruns (Basic) or balance alerts and overdue receivables (Pro).
5. **Forecast node** — project cash flow for the next 30 / 60 / 90 days.
6. **Advice-generation node** — local Ollama inference produces bilingual (EN/ZH) recommendations.
7. **Tax-RAG node (Pro, supporting)** — vector-retrieve relevant tax provisions and return cited references.

---

## Development Roadmap

The project is built as a sequence of phases over roughly seven weeks. **Phase 0 builds a thin end-to-end "walking skeleton"**, then **the entire Basic tier ships before any Pro work begins** — it delivers immediate value and exercises the whole stack before business complexity is added. Tests, linting, and CI are set up in Phase 0 and maintained continuously. Treat this as the path to a usable **v0.1**, with full payroll and the AI engine as stretch goals.

| Phase | Timeline | Tier | Deliverable |
|-------|----------|------|-------------|
| **Phase 0** | Week 1 (first half) | — | Walking skeleton: one transaction end-to-end (Electron → FastAPI → SQLite → React) + test / lint / CI scaffolding |
| **Phase 1** | Weeks 1–2 | 🟢 Basic | **Personal ledger complete** — books, accounts, categories, transactions (`INCOME`/`EXPENSE`/`TRANSFER`), fast capture, budgets & alerts, need/want, spending analysis, `Decimal` money, derived balances, CSV export, automatic backup. Unit & property tests written alongside. **Basic tier is shippable at the end of this phase.** |
| **Phase 2** | Week 3 | 🔵 Pro | Accounting core: chart of accounts, vouchers/journal, double-entry posting with **balance validation**, trial balance, Pro-mode toggle |
| **Phase 3** | Week 4 | 🔵 Pro | Business module APIs by value: revenue / cost / AR / AP, then assets, then payroll (**SG CPF first, CN later**) |
| **Phase 4** | Week 5 | 🔵 Pro | Three-statement generation (built on the trial balance) + Excel/PDF export |
| **Phase 5** | Week 6 | Both | Ollama integration + LangGraph AI analysis engine (minimal, supporting) |
| **Phase 6** | Week 7 | 🔵 Pro | Tax RAG knowledge base (reference) + full end-to-end testing, code-signing & packaging |

---

## Final Deliverables

On completion, the project ships as directly installable desktop packages — **one build containing both tiers**:

- `FinLedger-Pro-Mac.dmg` — macOS installer
- `FinLedger-Pro-Win.exe` — Windows installer
- `FinLedger-Pro-Linux.AppImage` — Linux installer

**Post-install experience:**

- Double-click the icon to launch; the FastAPI service and Ollama model start automatically in the background.
- Opens in **Basic mode** — personal bookkeeping, ready to use immediately with no setup.
- **Pro mode** is enabled with a single settings toggle whenever business accounting is needed.
- No server configuration and no internet connection required — works out of the box.
- All data is stored in a local SQLite file the user can back up freely.
- The tax knowledge base can be updated with a built-in one-click tool (requires internet).
- The interface supports switching between Chinese and English.

---

## Companion Finance Learning Path

This project is built as a **teaching project**: the author writes the code themselves, paced alongside a structured finance & accounting curriculum. Each week of learning maps directly onto the software module being built, so theory is applied immediately.

| Week | Learning Topic | Corresponding Module | Tier |
|------|----------------|----------------------|------|
| **Week 1** | Personal cash flow, categories, budgeting, entity assumption | Personal ledger | 🟢 Basic |
| **Week 2** | The five accounting elements + debit/credit rules | Accounting core (chart of accounts, journal) | 🔵 Pro |
| **Week 3** | Revenue recognition + cost accounting | Revenue module + Cost module | 🔵 Pro |
| **Week 4** | Receivables/payables + aging analysis | AR/AP module | 🔵 Pro |
| **Week 5** | Payroll calculation (SG CPF + CN 五险一金 + piece-rate) | Payroll module | 🔵 Pro |
| **Week 6** | Fixed-asset depreciation + comprehensive three-statement exercises | Fixed assets + statement generation | 🔵 Pro |

---

## Project Conventions

This repository follows a **teaching-mode** workflow:

- **All documentation is written in English.**
- **All code comments are written in English.**
- **Teaching and discussion happen bilingually (Chinese + English).**
- **The author writes all the code personally** — this repo is a learning vehicle, not a code-generation target. Assistance is for guidance, review, and explanation, not for writing the implementation.
- **Finance concepts are taught alongside the build** — each feature starts with the accounting concept, then the implementation, then a review that ties the code back to the concept.

---

## Planned Repository Structure

> Indicative layout — to be created as the project is built phase by phase. Note how `core/` is shared and the two tiers sit beside each other as feature layers.

```
FinLedgerPro/
├── electron/                # Electron main process, app lifecycle, backend bootstrap
├── frontend/                # React + Tailwind UI
│   └── src/
│       ├── core/            # Shared UI: money input, tables, layout, i18n
│       ├── personal/        # 🟢 BASIC tier screens: capture, budgets, analysis
│       └── pro/             # 🔵 PRO tier screens: journal, statements, modules
├── backend/                 # Python FastAPI service
│   ├── core/                # Shared kernel — books, accounts, Decimal money,
│   │                        #   transactions, audit trail, config, migrations
│   ├── personal/            # 🟢 BASIC tier: categories, budgets, spending analysis
│   ├── pro/                 # 🔵 PRO tier
│   │   ├── accounting/      #   chart of accounts, journal, posting, trial balance
│   │   ├── modules/         #   revenue, cost, ar_ap, payroll, assets, profit
│   │   ├── statements/      #   P&L, Balance Sheet, Cash Flow + Excel/PDF export
│   │   └── tax_rag/         #   ChromaDB + RAG tax-knowledge lookup
│   ├── ai/                  # LangChain / LangGraph workflow + Ollama (both tiers)
│   └── db/                  # SQLite schema, migrations, data access
├── data/                    # Local SQLite file, FX cache, tax PDFs (gitignored)
├── docs/                    # English documentation
├── tests/                   # Unit, property, integration, and E2E tests
├── LICENSE                  # MIT
└── README.md
```

**Dependency rule:** `personal/` and `pro/` may both depend on `core/`; **neither may depend on the other**. This keeps Basic fully functional with Pro absent, and keeps the tier boundary from eroding over time.

---

## What Makes It Production-Grade

"Production-grade" does not mean *more features* — it means **people can trust real money and real decisions to the software**. For a local-first finance tool, that trust rests on six pillars. This section is the engineering standard the project is built to.

### 1. Correctness & Financial Integrity

- **Money is `Decimal`, never `float`.** Floating-point cannot represent `0.1` exactly; using it for currency produces rounding errors that break reconciliation. All monetary values use fixed-precision decimal types end to end (Python `Decimal`, `NUMERIC` in SQLite, string-based transport in JSON).
- **Double-entry must balance.** *(Pro.)* Every posted journal entry is validated so total debits equal total credits before commit. An unbalanced entry is rejected, not stored.
- **Records are immutable + audit trail.** Posted entries are never edited or deleted in place; corrections are made via reversing entries. Every record carries `created_at`, `created_by`, and a reason.
- **Deterministic rounding.** Currency conversion and tax math use explicit, documented rounding rules (e.g. banker's rounding, 2 decimal places) so results are reproducible.
- **ACID transactions.** Multi-step postings run inside a single database transaction — all succeed or all roll back.

### 2. Testing & Quality Gates

- **Unit tests** for the accounting engine, currency conversion, depreciation, and payroll math — high coverage on the financial core specifically.
- **Property-based tests** for invariants (e.g. "debits always equal credits", "balance sheet always balances", "transfers never change net worth").
- **Integration tests** for the FastAPI endpoints against a real temporary SQLite database.
- **End-to-end tests** for the Electron app (e.g. Playwright) covering the critical user flows in both tiers.
- **Golden-file tests** for generated statements and Excel/PDF exports.
- **Static quality:** linting (`ruff` / `eslint`), formatting (`black` / `prettier`), type checking (`mypy` strict, TypeScript `strict: true`), enforced via pre-commit hooks and CI.

### 3. Security & Privacy

- **Encryption at rest.** The SQLite database is encrypted (e.g. SQLCipher) and unlocked by a user passphrase — losing the laptop must not mean losing the books.
- **Localhost-only backend.** The embedded FastAPI service binds to `127.0.0.1` only and is protected by a per-session token shared with the Electron process.
- **Strict input validation.** All API input is validated with Pydantic schemas; nothing untrusted reaches the database.
- **Signed installers.** macOS builds are code-signed and notarized; Windows builds are code-signed.
- **Dependency hygiene.** Dependencies are pinned (lockfiles) and scanned for known vulnerabilities in CI.
- **No telemetry, ever.** The app ships with no analytics; any future telemetry would be strictly opt-in and local-only.

### 4. Reliability & Data Safety

Because all data lives in one local SQLite file, **data loss is the single biggest risk** — this gets first-class treatment.

- **Schema migrations.** Schema changes are versioned and applied via a migration tool (e.g. Alembic) so upgrading never corrupts existing books.
- **Automatic backups.** Timestamped local backups on a schedule and before every migration, with one-click restore.
- **Integrity checks.** On startup the app runs `PRAGMA integrity_check` and verifies the books still balance; problems are surfaced, not hidden.
- **Crash recovery.** Write-ahead logging (WAL) and atomic writes ensure an interrupted save never leaves a half-written ledger.
- **Graceful degradation.** If the AI model or exchange-rate refresh is unavailable, core bookkeeping keeps working.

### 5. Build, Release & Updates

- **CI/CD pipeline.** Every change runs tests, linting, and type checks; tagged releases build and package the three installers automatically.
- **Semantic versioning + changelog.** Releases follow `MAJOR.MINOR.PATCH` with a maintained `CHANGELOG.md`.
- **Auto-update.** The desktop app supports safe in-place updates (e.g. `electron-updater`).
- **Reproducible builds.** Locked dependency versions and pinned toolchains so a given tag always builds the same artifact.

### 6. Observability & Supportability

- **Structured logging.** The backend logs in structured form (JSON), with levels, to local rotating log files — never logging sensitive financial values.
- **User-visible error reporting.** Errors surface as clear, actionable bilingual messages, not silent failures or raw stack traces.
- **Diagnostics export.** A built-in tool bundles logs and environment info (no financial data) to make support possible for a local app.

---

## Financial Correctness Rules (Non-Negotiable)

These are domain rules that distinguish a real accounting system from a generic CRUD app. **Violating any of them produces wrong numbers**:

1. **Use `Decimal` for every monetary amount.** Never `float`, never binary floating point — anywhere, including intermediate calculations.
2. **`TRANSFER` is never spending.** *(Basic.)* Moving money between your own accounts — including credit-card repayment — must be excluded from expense totals and budgets, or spending is double-counted.
3. **Debits = Credits, always.** *(Pro.)* Reject any journal entry that does not balance.
4. **Assets = Liabilities + Equity, always.** *(Pro.)* If the balance sheet does not reconcile, that is a bug, not a rounding artifact.
5. **Balances are derived, not stored.** Compute from the transaction history; a mutable balance column inevitably drifts.
6. **Post, don't mutate.** Correct mistakes with reversing entries; never silently edit a posted record.
7. **One source of truth for FX.** Store the exchange rate used *on each transaction*, so historical reports don't change when today's rate changes.
8. **Round once, explicitly, and at the boundary.** Define where rounding happens and to how many decimals; never let it happen implicitly mid-calculation.
9. **Separate "recognized" from "received".** *(Pro.)* Revenue recognition and cash receipt are different events — model them separately (accrual vs cash).
10. **Never merge personal and business books.** The entity assumption is enforced structurally, not by convention.

---

## Production Readiness Checklist

A pragmatic "definition of done". Items are targets for the build, not yet implemented.

| Category | Item | Target |
|----------|------|--------|
| **Correctness** | `Decimal` money everywhere | ☐ |
| **Correctness** | `TRANSFER` excluded from spending totals | ☐ |
| **Correctness** | Balanced-entry validation (Pro) | ☐ |
| **Correctness** | Property tests for accounting invariants | ☐ |
| **Testing** | Engine unit coverage ≥ 90% | ☐ |
| **Testing** | E2E tests for critical flows in both tiers | ☐ |
| **Architecture** | `personal/` and `pro/` have no mutual dependency | ☐ |
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

🚧 **In development — at Phase 0, building not yet started.**

**Decided / done**
- ✅ Positioning restructured into two free tiers: **Basic (personal)** and **Pro (business)**.
- ✅ Scope, architecture, and tier boundary defined (this document + [docs/architecture.md](docs/architecture.md)).
- ✅ Tech stack chosen (Electron + React/Tailwind + FastAPI + Ollama/LangGraph + SQLite + ChromaDB).
- ✅ Licensed under **MIT** — everything free and open source, no paid tier.
- ✅ Engineering standards and financial-correctness rules agreed.
- ✅ Roadmap sequenced so the Basic tier ships complete before Pro work begins.

**Not started yet**
- ⬜ No application code written — the repository currently holds only documentation and the license.
- ⬜ Phase 0 walking skeleton is the immediate next step.

**Next step:** Phase 0 — scaffold the repo per the structure above and get a single personal transaction flowing end-to-end (Electron → FastAPI → SQLite → React), with `Decimal` money and the test/CI harness in place from day one.

This is a **teaching project**: the author writes all code personally (see [Project Conventions](#project-conventions)). The production-readiness items above are targets to build toward, not yet implemented.

---

## Documentation

| Document | What it covers |
|----------|----------------|
| [README](README.md) | Positioning, the Basic/Pro tiers, features, tech stack, roadmap, engineering standards |
| [docs/architecture.md](docs/architecture.md) | The narrow-waist architecture ADR — kernel, tier layering, extensibility design points, worked example |
| [CHANGELOG.md](CHANGELOG.md) | What has been decided and built, by release |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to report bugs and give feedback on a teaching project |
| [LICENSE](LICENSE) | MIT |

---

## Contributing

Bug reports, design critique, **accounting corrections**, and documentation fixes are very welcome. Feature and refactoring pull requests are respectfully declined — this is a teaching project in which the author writes all application code personally, and outside implementations would defeat its purpose.

The project is MIT-licensed, so **forking is a first-class option** if you want to take it in your own direction. See [CONTRIBUTING.md](CONTRIBUTING.md) for details, including how to report issues without exposing real financial data.

---

## License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for the full text.

MIT is a short, permissive license: anyone may use, copy, modify, merge, publish, distribute, sublicense, and sell the software — including in closed-source and commercial products — as long as they keep the original copyright and license notice. The software is provided "as is", without warranty.

**Both tiers are covered.** Basic and Pro are published under the same licence, at no cost. There is no proprietary edition and nothing is withheld.

## Acknowledgements

- Project summary and positioning authored with assistance from Claude (Anthropic), 2026.

---

*FinLedger Pro — Own your finances, own your data, own your decisions.*
