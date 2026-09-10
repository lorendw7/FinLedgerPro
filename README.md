# FinLedger Pro

[English](README.md) | [简体中文](README.zh-CN.md)

**A free, open-source, local-first accounting core and reference app — ready for personal use and private company customisation.**

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
- [Learning from Xero](#learning-from-xero)
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
- **Pro — Business accounting.** Full double-entry accounting for a startup or micro-business: chart of accounts, connected operating workflows, three financial statements, dual-market payroll (Singapore + China), AI analysis, and tax-knowledge lookup. Switched on when you need it.

Every piece of core accounting data lives on the user's own machine — no mandatory cloud service, hosted account, or subscription. **Both tiers and the reusable public core are completely free and MIT-licensed** (see [Everything Is Free and Open Source](#everything-is-free-and-open-source)). A company may keep its own branding, mappings, workflows, and provider configuration in a separate private repository that depends on a released public-core version.

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

The maintainer has no plan to commercialise the public project. FinLedger Pro's reusable accounting core and reference application remain public and open source; “Pro” will never become a paid edition.

The project's permanent upstream rules are recorded in the [Open-Source and Free-Forever Commitment](OPEN_SOURCE_COMMITMENT.md): the repository remains public, official releases remain MIT-licensed, local accounting features remain free, and no public feature is withheld for a proprietary FinLedger Pro edition.

- The complete source code — Basic *and* Pro — is published under the **[MIT License](LICENSE)**.
- "Pro" denotes an **advanced feature set**, not a commercial edition. Enabling it is a settings toggle, not a purchase.
- This is **not** an open-core sales model: the maintainer withholds no proprietary paid tier. Downstream companies may still keep their own company-specific extension repositories private.
- Anyone may use, modify, redistribute, or build commercial products on top of the code, provided the copyright notice is retained.

The supported customisation model is **company private repository → tagged public-core release**, not a long-lived private fork. See [Public Core and Private Company Repositories](docs/public-core-and-private-company-repos.md).

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
3. **A fully open public foundation.** Every feature shipped by this repository is MIT-licensed and free. Companies may own private downstream extensions without turning the upstream project into a paid open-core product.
4. **Progressive disclosure.** Complexity appears only when asked for. Basic hides everything a personal user does not need; Pro reveals it on request.
5. **Offline by default, online by exception.** Optional online touchpoints are exchange-rate refresh, tax-knowledge updates, and read-only bank feeds. All are replaceable, cached where appropriate, and never required to open or operate the books.
6. **Accounting-correct.** The Pro kernel implements proper double-entry bookkeeping so the three statements can be generated to standard.
7. **Dual-market native.** Singapore and China differences are first-class concepts in the data model, not afterthoughts.
8. **AI as an assistant, not an authority.** AI provides analysis, forecasts, and *cited* tax references — it never files taxes or makes binding decisions.
9. **Educational by design.** Built as a structured learning vehicle: phases map onto a finance & accounting curriculum (see [Companion Finance Learning Path](#companion-finance-learning-path)).
10. **Open interfaces, replaceable providers.** Optional network features use open standards and pluggable adapters, with a manual/offline path always available.

---

## Learning from Xero

[Xero](https://www.xero.com/us/accounting-software/) is a mature cloud accounting platform for small and medium-sized businesses. FinLedger Pro studies Xero as a **workflow and control benchmark**, not as a product to clone.

The most valuable pattern is the connected daily loop:

```text
contacts → invoices / bills → receipt and payment records → bank reconciliation → reports
```

FinLedger Pro adopts the underlying product lessons while preserving its own position:

| Learn from Xero | FinLedger Pro adaptation |
|---|---|
| Bank reconciliation as a frequent, central task | Local CSV / OFX / QIF first; read-only bank feeds use the same staging and reconciliation path |
| Source-document workflows | Bills, invoices, settlements, and externally evidenced payment records generate immutable journal entries |
| Contact-level financial history | One party record links AR, AP, payments, projects, and documents |
| Project profitability and tracking dimensions | First-class annotation-project revenue, accepted-output cost, and margin |
| Lock dates and history / notes | Period close controls and an append-only audit trail |
| Fast automation with review | Rules suggest; the owner approves; AI cannot post autonomously in v1 |

The detailed research, official references, product decisions, and study exercises are in [docs/xero-product-benchmark.md](docs/xero-product-benchmark.md). The quality-gated implementation sequence is in [docs/product-roadmap.md](docs/product-roadmap.md).

FinLedger Pro is **not affiliated with, endorsed by, or derived from Xero source code**. It learns from publicly documented accounting workflows such as bank reconciliation, contact histories, project profitability, lock dates, and audit trails; no Xero code, branding, screenshots, or proprietary assets are used.

---

## Scope: What It Is / What It Is Not

| ✅ FinLedger Pro **is** | ❌ FinLedger Pro **is not** |
|------------------------|----------------------------|
| A free, MIT-licensed, local desktop finance tool | A cloud / SaaS service, or a paid product |
| Two tiers in one app: personal (Basic) + business (Pro) | An open-core product with a proprietary paid edition |
| Single-user, owned by the person running it | A multi-user team or accounting-firm platform |
| A tool that *records, reconciles, reports, and analyzes* finances | A **tax-filing** or statutory-submission system |
| A system that imports read-only bank transactions and records settlements | A payment initiator, payout service, card platform, or bank-control interface |
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
| **Open integration layer** | Provider adapters + local cache | FX and read-only bank feeds; every provider remains replaceable and no payment methods are exposed |
| **Currency data** | Manual rates + Frankfurter / ECB candidates | ISO 4217 multi-currency model; SGD/CNY first; historical rate snapshots |

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

### The business capability groups

The Pro tier covers the full operational accounting chain.

| Module | Capabilities | Region |
|--------|--------------|--------|
| **Revenue Recognition** | Contract management, deferred/installment amortization, three-state tracking (invoiced / received / recognized) | SG + CN |
| **Cost Accounting** | Direct/indirect cost classification, project allocation, automatic gross-margin calculation | SG + CN |
| **Receivables & Payables (AR/AP)** | Invoice tracking, aging analysis (30/60/90 days), overdue alerts, payment schedules | SG + CN |
| **Workforce Settlement & Payroll** | Piece-rate contractor settlement first; Singapore CPF / China 五险一金 employee payroll later | SG / CN |
| **Fixed-Asset Depreciation** | Straight-line / double-declining-balance methods, monthly auto-accrual, asset register | SG + CN |
| **Profit Analysis** | Three-tier analysis (gross / operating / net profit), 12-month trend, AI interpretation | SG + CN |
| **Banking & Reconciliation** | File/API statement import, duplicate detection, matching, recorded transfers, reconciliation evidence, and difference reporting; read-only, with no payment initiation | SG + CN |

---

## Single-Entry vs Double-Entry Bookkeeping

**Single-entry** (Basic) — like a bank statement: records date, amount, category, and running balance. Best for fast entry of day-to-day income and expenses; simple and intuitive.

**Double-entry** (Pro) — follows the debit/credit principle (*every debit must have a matching credit; debits must equal credits*). Strictly aligned with accounting standards and supports automatic generation of the three financial statements. Best when the books must be reported externally or audited.

Turning on Pro mode does not migrate or convert the personal book — the two remain separate sets of books, as the entity assumption requires.

---

## Dual-Currency & Dual-Market Support

### Currency Handling

- Model currencies with ISO 4217 codes. **SGD and CNY are the first fully tested currencies**, while the data model and provider interface support additional currencies without schema changes.
- Every book has a **functional currency**; every transaction preserves its original currency and amount plus the functional-currency amount.
- Every conversion stores a rate snapshot: provider, rate date, retrieval time, quote convention, and whether the user overrode it. Historical reports never change when a later rate is downloaded.
- Manual rates are always available. Optional online rates use a replaceable provider adapter and a local cache; bookkeeping continues when every API is offline.
- The first provider candidates are [Frankfurter](https://frankfurter.dev/) (open source and self-hostable) and the [ECB Data API](https://data.ecb.europa.eu/help/getting-data-web-services-sdmx-0) (official reference data). Reference rates are suggestions, not automatically authoritative tax or transaction rates.
- Reports may use the book's functional currency or a selected presentation currency. Pro later adds realized/unrealized FX treatment and multi-entity consolidation.

The full provider policy, data contract, fallback behavior, and accounting rules are documented in [docs/open-api-and-multi-currency.md](docs/open-api-and-multi-currency.md).

### Singapore vs China Business Differences

| Item | Singapore | China |
|------|-----------|-------|
| **Primary currency** | SGD | CNY |
| **Payroll & social security** | CPF eligibility and effective-dated rates depend on worker status, age, wage type, and statutory limits | Five-Insurances-One-Fund eligibility, bases, and rates vary by locality and effective period |
| **Tax reference** | Effective-dated Singapore GST and corporate-tax reference rules | Effective-dated China VAT and corporate-tax reference rules by taxpayer and transaction type |
| **Financial year** | Apr–Mar or Jan–Dec (selectable) | Jan–Dec |
| **Report language** | Bilingual (EN/ZH) | Chinese |

> Tax and contribution rules are versioned reference configuration—not permanent constants and not official filing guidance. Every calculation preserves the jurisdiction, effective date, source, and rule version used.

### Payroll & Social Contributions (the hardest module)

Payroll is the most complex Pro module because **statutory social-contribution rules differ by jurisdiction, change every year, and depend on more than a flat percentage of salary**. The system therefore models both schemes with **configurable rates** (stored in editable configuration, not hard-coded), so the user can update them when policy changes without a new release.

**Singapore — CPF (Central Provident Fund / 中央公积金):**
A mandatory retirement, housing, and healthcare savings scheme. Employer and employee obligations depend on worker status, age band, wage type, statutory ceilings, and the rule's effective date; allocations are made across CPF accounts. The implementation must obtain current rules from an authoritative source and preserve the exact rule version used for every completed calculation.

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

All rates and contribution bases stay in effective-dated, source-attributed configuration so they can be updated per locality and period without a code change while historical results remain reproducible. A configured label does not determine the legal nature of a working relationship; classification depends on the actual facts and applicable law. *(Rules above are general reference, not legal advice—confirm with CPF Board / IRAS / MOM, the local 人社局, tax authorities, or a qualified professional before acting.)*

**Why statutory employee payroll is deferred:** the rules are external, locale-specific, and frequently updated, making this the most error-prone capability and the one most coupled to policy. The actual data-annotation need—piece-rate contractor settlement—is built first. If employee payroll is later required, Singapore CPF is validated before China's locality-dependent rules. A worked example of the piece-rate 劳务 flow is in [docs/architecture.md](docs/architecture.md#9-worked-example-data-annotation-piece-rate-flow).

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

The roadmap now uses **quality-gated milestones instead of a seven-week deadline**. A single developer learning accounting should not trade correctness or recoverability for calendar speed. The first priority is a complete business workflow that the owner can reconcile and close; broad features and AI follow only after the books are trustworthy.

| Milestone | Focus | Release gate |
|---|---|---|
| **M0 — Definition** | Positioning, architecture, Xero benchmark, scope, and reliability rules | Documents agree on terminology, boundaries, sequence, and non-goals |
| **M1 — Local foundation** | Walking skeleton, separate books, `Decimal`, migrations, audit events, idempotency, backup and restore | Crash, retry, integrity, and clean-restore tests pass |
| **M2 — Accounting kernel** | Chart of accounts, source-document lifecycle, balanced posting, trial balance, opening balances, period locks | Posted history is immutable; trial balance reproduces the journal; closed periods reject changes |
| **M3 — Spend to reconcile** | Contacts, bills, annotation output and contractor settlement, AP, bank-file import, read-only bank-feed contract, reconciliation, Action Center | Accepted output → settlement → payable → externally executed payment → imported transaction → reconciliation → cost report works without a spreadsheet |
| **M4 — Earn to reconcile** | Contracts/projects, invoices, credit notes, AR, receipts, aging, project margin | Client job → invoice → receipt → reconciliation → margin handles partial payment and cancellation safely |
| **M5 — Close and report** | Month-end checklist, three statements, reconciliation report, drill-down, fixed assets, export | Every balance traces to evidence; a closed month reproduces after restore |
| **M6 — SG/CN scale** | SGD/CNY, effective-dated FX, multi-entity isolation, intercompany and consolidation | Historical reports remain stable; entity isolation and consolidation invariants pass |
| **M7 — Basic completion** | Personal capture, budgets, credit cards, transfers, net worth, spending analysis | Transfers never become spending; personal and business books remain isolated |
| **M8 — Production RC** | Encryption, supply-chain checks, full test matrix, diagnostics, signed installers, upgrade/rollback | All production gates pass plus one full parallel shadow-book close |
| **M9 — Optional intelligence** | Rules, forecasts, local AI, tax RAG, and selected read-only integrations | Disabling AI or a provider changes no accounting result; no integration can initiate a payment |

The detailed deliverables, finance lessons, acceptance gates, version labels, and safe adoption process are maintained in [docs/product-roadmap.md](docs/product-roadmap.md).

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

This project is a **teaching project**: the author writes all implementation code personally. Each milestone begins with finance theory, applies it in a small implementation, and ends by reconciling the code's output to a worked accounting example.

| Milestone | Finance lesson | Applied software work |
|---|---|---|
| **M1** | Entity assumption, monetary precision, source evidence, and internal control | Separate books, `Decimal`, audit trail, backup / restore |
| **M2** | Five accounting elements, debit / credit rules, accrual basis, and opening balances | Chart of accounts, journal, posting, trial balance, period locks |
| **M3** | Expenses vs assets, AP, cost recognition, withholding, and reconciliation | Bills, piece-rate contractor settlements, bank import and matching |
| **M4** | Revenue recognition, AR, credit notes, deposits, and partial payments | Invoices, receipts, aging, project revenue and margin |
| **M5** | Accruals, prepayments, depreciation, month-end close, and the three statements | Closing checklist, reports, drill-down and exports |
| **M6** | Functional currency, realized / unrealized FX, intercompany, and consolidation | SGD/CNY books, FX snapshots, entity isolation and consolidated reports |
| **M7** | Cash budgeting, credit-card liabilities, transfers, net worth, and savings rate | Complete Basic personal-finance experience |
| **M8** | Threat modeling, recovery objectives, software supply chain, and release controls | Production hardening and shadow-book validation |
| **M9** | Forecast uncertainty, explainable automation, and retrieval quality | Local AI and tax-reference assistance after accounting is stable |

---

## Project Conventions

This repository follows a **bilingual teaching-mode** workflow:

- **Reader-facing documentation is maintained in paired English and Simplified Chinese editions.** English is the canonical technical wording when the two differ; every major document links to its counterpart.
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
│   ├── integrations/        # Replaceable FX and read-only bank-feed contracts
│   └── db/                  # SQLite schema, migrations, data access
├── data/                    # Local SQLite file, FX cache, tax PDFs (gitignored)
├── docs/                    # English architecture, roadmap, research, and runbooks
├── tests/                   # Unit, property, integration, and E2E tests
├── LICENSE                  # MIT
└── README.md
```

**Dependency rule:** `personal/` and `pro/` may both depend on `core/`; **neither may depend on the other**. This keeps Basic fully functional with Pro absent, and keeps the tier boundary from eroding over time.

Company-specific software lives in a separate private repository and consumes a tagged release of this public core. It may add company branding, account mappings, invoice layouts, internal workflows, and read-only providers such as Aspire, but it must not copy credentials or financial data into Git. The public core never depends on private company code. The complete boundary and upgrade rules are in [Public Core and Private Company Repositories](docs/public-core-and-private-company-repos.md).

---

## What Makes It Production-Grade

"Production-grade" does not mean *more features* — it means **people can trust real money and real decisions to the software**. For a local-first finance tool, that trust rests on six pillars. This section is the engineering standard the project is built to.

### 1. Correctness & Financial Integrity

- **Money is `Decimal`, never `float`.** Floating-point cannot represent `0.1` exactly; using it for currency produces rounding errors that break reconciliation. All monetary values use fixed-precision decimal types end to end (Python `Decimal`, `NUMERIC` in SQLite, string-based transport in JSON).
- **Double-entry must balance.** *(Pro.)* Every posted journal entry is validated so total debits equal total credits before commit. An unbalanced entry is rejected, not stored.
- **Records are immutable + audit trail.** Posted entries are never edited or deleted in place; corrections are made via reversing entries. Every record carries `created_at`, `created_by`, and a reason.
- **Deterministic rounding.** Currency conversion and tax math use explicit, documented rounding rules (e.g. banker's rounding, 2 decimal places) so results are reproducible.
- **ACID transactions.** Multi-step postings run inside a single database transaction — all succeed or all roll back.
- **Idempotent commands.** Repeating the same create, post, settle, pay, or import command has one financial effect, never two.
- **Controlled document states.** Source documents move through explicit draft, approval, posting, payment/settlement, and reversal states; invalid transitions are rejected.

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
- **Verified restore.** Backup health includes a periodic automated restore-and-open test; a file that has never been restored is not yet a trusted backup.
- **Integrity checks.** On startup the app runs `PRAGMA integrity_check` and verifies the books still balance; problems are surfaced, not hidden.
- **Crash recovery.** Write-ahead logging (WAL) and atomic writes ensure an interrupted save never leaves a half-written ledger.
- **Duplicate-safe imports.** Bank files and statement lines are fingerprinted and staged before posting, preventing accidental duplicate cash movements.
- **Reconciliation and close controls.** Bank differences remain visible until resolved; closed periods reject changes unless an explicit, audited unlock occurs.
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
| **Correctness** | Idempotent posting, payment-recording, settlement, and import commands | ☐ |
| **Workflow** | Draft → approve → post → reverse state controls | ☐ |
| **Workflow** | Source document → journal → report drill-down | ☐ |
| **Workflow** | Bank import staging, duplicate detection, and reconciliation evidence | ☐ |
| **Workflow** | Period lock and month-end close checklist | ☐ |
| **Testing** | Engine unit coverage ≥ 90% | ☐ |
| **Testing** | E2E tests for critical flows in both tiers | ☐ |
| **Architecture** | `personal/` and `pro/` have no mutual dependency | ☐ |
| **Security** | Encrypted SQLite (passphrase) | ☐ |
| **Security** | Localhost-only API + session token | ☐ |
| **Security** | Signed & notarized installers | ☐ |
| **Reliability** | Versioned DB migrations | ☐ |
| **Reliability** | Automatic backups + one-click restore | ☐ |
| **Reliability** | Automated restore verification | ☐ |
| **Reliability** | Startup integrity + balance check | ☐ |
| **Integration** | Manual/offline path for every optional API | ☐ |
| **Integration** | Provider contract tests, timeout/retry limits, cache provenance, and stale-data warning | ☐ |
| **Integration** | Read-only bank-feed contract; no transfer, payout, beneficiary, card, or collection methods | ☐ |
| **Currency** | ISO 4217 model + SGD/CNY acceptance tests | ☐ |
| **Currency** | Per-transaction rate snapshot + realized/unrealized FX tests | ☐ |
| **Release** | CI runs tests/lint/types on every change | ☐ |
| **Release** | Auto-update for the desktop app | ☐ |
| **Release** | SemVer + maintained changelog | ☐ |
| **Observability** | Structured local logs (no sensitive data) | ☐ |
| **Docs** | API docs (OpenAPI), ADRs, runbook | ☐ |

---

## Project Status

🚧 **In development — M0 design is complete; M1 implementation has not started.**

**Decided / done**
- ✅ Development baseline pinned: Node 24.14, pnpm 11.9, CPython 3.13, uv-managed virtual environment, and reproducible lockfiles.
- ✅ Positioning restructured into two free tiers: **Basic (personal)** and **Pro (business)**.
- ✅ Scope, architecture, and tier boundary defined (this document + [docs/architecture.md](docs/architecture.md)).
- ✅ Xero studied as a workflow/control benchmark; adoption and non-copy decisions documented.
- ✅ Full open-source / no-commercialisation intent and Xero non-affiliation documented.
- ✅ Open-API and multi-currency provider strategy defined; SGD/CNY remain the first acceptance target.
- ✅ Tech stack chosen (Electron + React/Tailwind + FastAPI + Ollama/LangGraph + SQLite + ChromaDB).
- ✅ Licensed under **MIT** — everything free and open source, no paid tier.
- ✅ Engineering standards and financial-correctness rules agreed.
- ✅ Roadmap changed from a seven-week feature schedule to quality-gated product milestones focused on real-book reliability.

**Not started yet**
- ⬜ No application code written — the repository currently holds only documentation and the license.
- ⬜ M1 trustworthy local foundation is the immediate next step.

**Next step:** M1 — scaffold the repo per the structure above and get one personal transaction plus one business source document flowing end-to-end (Electron → FastAPI → SQLite → React), with `Decimal`, idempotency, audit events, migrations, test/CI, backup, and restore in place from day one.

This is a **teaching project**: the author writes all code personally (see [Project Conventions](#project-conventions)). The production-readiness items above are targets to build toward, not yet implemented.

---

## Documentation

| Document | What it covers |
|----------|----------------|
| [README](README.md) · [中文](README.zh-CN.md) | Positioning, feature tiers, engineering standards, and project status |
| [Documentation index](docs/README.md) | Bilingual documentation map and language policy |
| [Development setup](docs/development-setup.md) · [中文](docs/development-setup.zh-CN.md) | Pinned tools, local environment creation, lockfiles, and secrets boundary |
| [Architecture](docs/architecture.md) · [中文](docs/architecture.zh-CN.md) | Narrow-waist architecture, boundaries, and worked example |
| [Xero benchmark](docs/xero-product-benchmark.md) · [中文](docs/xero-product-benchmark.zh-CN.md) | Xero-inspired workflows, adaptation decisions, and non-affiliation |
| [Product roadmap](docs/product-roadmap.md) · [中文](docs/product-roadmap.zh-CN.md) | Quality-gated milestones, finance lessons, and safe adoption |
| [Open API & multi-currency](docs/open-api-and-multi-currency.md) · [中文](docs/open-api-and-multi-currency.zh-CN.md) | Provider architecture, currency data contract, fallback, and FX accounting |
| [Public core & private company repos](docs/public-core-and-private-company-repos.md) · [中文](docs/public-core-and-private-company-repos.zh-CN.md) | Downstream customisation, extension contracts, read-only banking, and secrets boundaries |
| [Open-source commitment](OPEN_SOURCE_COMMITMENT.md) · [中文](OPEN_SOURCE_COMMITMENT.zh-CN.md) | Permanent upstream licence, visibility, free-use, and no-paywall policy |
| [CHANGELOG.md](CHANGELOG.md) · [中文](CHANGELOG.zh-CN.md) | What has been decided and built, by release |
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

**Both tiers are covered.** Basic, Pro, and the reference application are published under the same licence, at no cost. The maintainer withholds no proprietary edition. A downstream company may keep its own extension repository private while depending on the public core.

**Project intent:** the maintainer has no plan to commercialise FinLedger Pro. There will be no subscription, paid edition, licence key, advertising, or feature paywall in the public project. The public core and reference application remain open source. The MIT License permits companies to build private or commercial downstream extensions; project intent does not remove rights granted by the licence.

See the [Open-Source and Free-Forever Commitment](OPEN_SOURCE_COMMITMENT.md) for the repository's non-negotiable upstream governance rules.

## Acknowledgements

- Project summary and positioning authored with assistance from Claude (Anthropic), 2026.
- Product workflow research draws on Xero's publicly available documentation. FinLedger Pro is an independent project and is not affiliated with or endorsed by Xero; no Xero source code or proprietary assets are included.

---

*FinLedger Pro — Own your finances, own your data, own your decisions.*
