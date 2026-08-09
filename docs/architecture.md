# FinLedger Pro — System Architecture

> **Status:** Design / Architecture Decision Record (ADR) · 2026
> **Audience:** the author (single developer) building FinLedger Pro phase by phase.
> **Goal of this document:** define a system shape that serves both a *personal* finance user and a *small company*, and can grow to meet the company's full needs over time — without ever rewriting the core.

---

## 1. The Design Goal

The application must satisfy two audiences that look very different:

- **A personal user** who wants to know where their money went and to spend less. Needs simplicity above all; must never be shown a debit or a credit.
- **A small company** whose accounting needs are open-ended: today paying part-time annotators, tomorrow invoicing clients, then bank reconciliation, fixed assets, payroll across two jurisdictions, tax.

Serving both with one codebase — without the personal experience drowning in accounting complexity, and without the business side being crippled by oversimplification — is the central design problem. **You also cannot build all of the business side up front.**

The answer has two parts:

1. A **narrow-waist architecture** — a small, correct, stable kernel with clean extension points, so every new business need is *"add a module that posts journal entries"* rather than *"re-architect the system"*.
2. **Two feature tiers layered on that one kernel** — Basic (personal) and Pro (business) — so complexity is revealed progressively.

---

## 2. Tier Layering: Basic and Pro on One Kernel

FinLedger Pro is organised into two feature tiers. **Both are free and MIT-licensed**; the tier boundary exists for progressive disclosure, not monetisation. There is no paywall and no licence key — Pro is a settings toggle.

```
   ┌──────────────────┐        ┌──────────────────┐
   │  🟢 personal/    │        │  🔵 pro/         │
   │  BASIC tier      │        │  PRO tier        │
   │  cash basis      │        │  accrual basis   │
   │  single-entry    │        │  double-entry    │
   └────────┬─────────┘        └────────┬─────────┘
            │                           │
            └───────────┬───────────────┘
                        ▼
              ┌───────────────────┐
              │      core/        │   books · accounts · Decimal money
              │  SHARED KERNEL    │   transactions · audit trail · db
              └───────────────────┘
```

**The dependency rule:** `personal/` and `pro/` may both depend on `core/`; **neither may depend on the other.** This is what keeps Basic fully functional when Pro is switched off, and stops the tier boundary from eroding as the codebase grows. It is enforced by directory structure and should be checked in CI.

### Where the boundary sits, and why

The line between the tiers is exactly the line between **single-entry cash-basis** and **double-entry accrual** bookkeeping. That is a real conceptual step, not an arbitrary product decision: below it, anyone can record a coffee purchase; above it, the user must understand that every debit needs a matching credit.

| | 🟢 Basic (`personal/`) | 🔵 Pro (`pro/`) |
|---|---|---|
| Book type | `PERSONAL` | `BUSINESS` (one per entity) |
| Basis | Cash basis (收付实现制) | Accrual basis (权责发生制) |
| Method | Single-entry | Double-entry (借 = 贷) |
| Record | `transaction` (income / expense / transfer) | Voucher + journal entries |
| Prerequisite knowledge | None | Debits and credits |

**Basic is not a trial version.** It is a complete personal-finance tool that happens to share a kernel with a business accounting system. It ships first and stands alone.

### What each tier contributes

- **`core/`** — books, accounts, `Decimal` money, transactions, audit trail, migrations, backup, config. Both tiers depend on it. This is the narrow waist.
- **`personal/`** — categories, budgets and alerts, need/want tagging, spending analysis, recurring detection, CSV export.
- **`pro/`** — chart of accounts, journal & double-entry posting, trial balance, the six business modules, three statements, tax RAG, Excel/PDF export.

---

## 3. The Core Idea: Narrow-Waist Architecture

![FinLedger Pro narrow-waist extensible architecture](architecture-narrow-waist.svg)

The key insight for the business side: **almost every business event a small company has — paying wages, issuing an invoice, paying a supplier, depreciating an asset, accruing tax — ultimately reduces to a single thing: posting a balanced journal entry (debit = credit).**

So the system has a fixed shape:

```
many business modules  →  ONE accounting ledger  →  many reports
   (they POST entries)        (the narrow waist)       (they READ it)
```

- The **ledger (accounting kernel)** is the *narrow waist*: the one component everything funnels through.
- **Business modules** are *subledgers* above the waist — they translate real-world events into journal entries and post them down.
- **Reporting & analysis** sits below the waist — it only ever reads the ledger.
- **Platform capabilities** wrap around all of it (multi-book, multi-entity, multi-currency, backup, security, import/export).

Get the waist right and **adding any future feature is cheap**: it never touches the core.

---

## 4. Why This Scales to "All the Needs of a Small Company"

Because the integration contract is tiny and universal: **a module's only job is to produce a balanced set of journal entries.** It does not need to know about reports, currencies, consolidation, or other modules. The ledger does not need to know what a module *means* — only that its entries balance.

This decoupling is what lets the system absorb unbounded requirements:

- A new business need → a new module + a posting rule. Core unchanged.
- A new report → a new read over the ledger. Core unchanged.
- A new jurisdiction or rate → a configuration change. Core unchanged.

---

## 5. The Four Layers

### 5.1 Business Modules (subledgers) — *they post entries*

Each module owns a real-world process and knows how to express it as journal entries. All of these are 🔵 Pro-tier except the personal ledger.

| Module | Tier | Responsibility |
|--------|------|----------------|
| **Personal Ledger** | 🟢 Basic | Personal accounts, categories, income/expense/transfer, budgets, spending analysis — its own `PERSONAL` book |
| Revenue & Invoicing | 🔵 Pro | Contracts, invoices, AR, receipts, revenue recognition |
| Expense & Payables | 🔵 Pro | Purchases/expenses, AP, payments, reimbursements |
| Payroll · piece-rate | 🔵 Pro | Employment types × pay methods, output records, settlements, tax withholding |
| Cost & Inventory | 🔵 Pro | Cost allocation, project cost, (optional) stock movements |
| Fixed Assets | 🔵 Pro | Asset register, depreciation accrual |
| Bank & Cash | 🔵 Pro | Bank accounts, cash movements, reconciliation |

### 5.2 Accounting Kernel (the narrow waist) — *the stable core*

The part that must be **correct above all else** and **change as rarely as possible**. Split between `core/` (used by both tiers) and `pro/accounting/` (double-entry machinery):

**`core/` — shared by both tiers**
- **Books** — each set of books (`PERSONAL`, and one per business entity) is isolated; only business books consolidate.
- **Accounts** — funds accounts and their derived balances.
- **Transactions & audit trail** — the immutable record of what happened, with `created_at` / `created_by`.
- Backed by **SQLite** (local file), **`Decimal`** money, and **ACID** transactions.

**`pro/accounting/` — Pro tier only**
- **Chart of Accounts** — the tree of accounts every journal entry is posted against.
- **General Ledger / Journal** — the double-entry book of record.
- **Double-entry posting** — validates `debits == credits` before commit; rejects unbalanced entries.
- **Trial Balance** — the bridge from journal to the three statements.

### 5.3 Reporting & Analysis — *they read the ledger*

- 🟢 Spending breakdown, savings rate, budget status, recurring-charge detection.
- 🔵 Three statements (P&L, Balance Sheet, Cash Flow), built on the trial balance.
- 🔵 Dashboards / KPIs, aging analysis.
- AI analysis (LangGraph + local Ollama) — serves both tiers.
- Export: 🟢 CSV · 🔵 Excel / PDF.

### 5.4 Platform (cross-cutting) — *wraps everything*

Multi-book & multi-entity (personal / SG / CN), multi-currency & consolidation, tax configuration (reference only), backup & restore, security/encryption, import/export, and configurable rates.

---

## 6. Capability Map — A Small Company's Full Needs

Every domain below is "just another subledger" that posts to the kernel. Priority is tailored to the project's actual workforce (data annotation, all part-time piece-rate workers — see [Section 8](#8-worked-example-data-annotation-piece-rate-flow)).

| Domain | Subledger module | Priority for this business |
|--------|------------------|----------------------------|
| **Personal finance** (🟢 Basic) | **Personal ledger — accounts, categories, transactions, budgets, spending analysis** | 🔴 **Highest — built first** (see [Section 6.1](#61-the-personal-ledger-basic-tier-separate-book-built-first)) |
| Expenditure cycle (P2P) | Expense/purchase, AP, payments, reimbursement | 🔴 High — pays annotators |
| Payroll | Employment-type × pay-method, output, settlement, tax | 🔴 High — 劳务 + piece-rate core |
| Revenue cycle (O2C) | Contract, invoice, AR, receipt, revenue recognition | 🔴 High — bills clients |
| Cash & banking | Accounts, cash flow, **bank reconciliation** | 🟠 Medium |
| Cost & profit | Project cost allocation, gross margin, profit analysis | 🟠 Medium |
| Fixed assets | Asset register, depreciation | 🟢 Low |
| Tax | Tax payable, VAT/GST, tax-knowledge RAG (reference) | 🟢 Low — start with lookup |
| Reporting & analysis | 3 statements, dashboards, AI, export | 🟠 Medium |

### 6.1 The personal ledger (Basic tier): separate book, built first

The personal ledger is the **entire Basic tier** and the **first thing built**, for two reasons: the owner has an immediate, concrete need (personal spending needs visibility and control), and it is the ideal **walking skeleton** — it exercises books, accounts, `Decimal` money, transactions, and reporting end to end without any business-domain complexity.

Architecturally it demonstrates why the narrow waist works: **it required no change to the kernel.** The `entity_id` / `book_id` extension point (§7.3) already anticipated multiple sets of books, so the personal ledger is simply another book.

**Separation is mandatory (entity assumption).** The owner and the company are distinct accounting entities; their books never merge. `book_type` distinguishes them:

| | `PERSONAL` | `BUSINESS` |
|---|---|---|
| Basis | Cash basis — recorded when money moves | Accrual basis |
| Method | Single-entry (cash-flow style) | Double-entry |
| Consolidation | **Never** consolidated with business books | Consolidated across SG + CN entities |

Money crossing the boundary is modelled explicitly, never as an expense in the wrong book:

| Situation | Correct treatment |
|-----------|-------------------|
| Company account pays a personal expense | Dr **Other receivable — shareholder** (loan to owner), not a company expense |
| Owner's own money pays a company cost | Cr **Other payable — shareholder** |
| Owner takes money out of the company | **Owner's draw / dividend / salary**, with an explicit nature |

**Three transaction kinds — `TRANSFER` is not spending.** The most common personal-bookkeeping error is counting a *movement* of money as *spending*:

- `INCOME` — money enters personal net worth.
- `EXPENSE` — money leaves personal net worth. **Only this counts toward spending totals and budgets.**
- `TRANSFER` — money moves between the user's own accounts (bank → e-wallet, or a **credit-card repayment**). Net worth is unchanged, so it is **excluded from all spending statistics**.

Credit cards are **liability accounts**: swiping is an expense *and* increases the liability; repayment is a `TRANSFER`. Counting both as expenses would double-count every card purchase.

**Balances are derived, never stored** — `opening_balance + Σ inflows − Σ outflows`. A stored, mutable balance drifts out of sync with the transactions; the transaction history is the single source of truth.

The full data-model blueprint and the spending-control feature set (fast capture, need-vs-want tagging, budgets with alerts, recurring-subscription detection, savings rate) are documented in the [README](../README.md#basic-tier--personal-ledger).

---

## 7. The Four Extensibility Design Points

These are what actually make "add anything later" cheap. They are non-negotiable foundations.

### 7.1 A unified posting interface (posting rules)
Every source document knows how to generate its own debits and credits. Adding a new kind of business event means writing **one new posting rule**, never touching the kernel.

```
settlement.post()   →  Dr  Labor cost            (expense)
                       Cr  Wages payable         (liability)
```

### 7.2 Configuration over code
Account mappings, tax rates, social-contribution rates, and piece rates live in **editable configuration/tables**, never hard-coded. When policy changes, the user edits data — not source — and ships no new release. The **Pro-mode toggle is configuration too**: enabling it mounts additional modules and routes rather than switching to a different application.

### 7.3 Multi-entity & multi-currency from day one
Operating in Singapore **and** China usually means **two legal entities, two sets of books, plus a consolidated view**. Every record carries an `entity_id` (or `book_id`) and a currency from the start — even while only one entity exists. Retrofitting this later is the single most expensive change to make, so it is designed in now, not bolted on.

### 7.4 Source documents + attachments + audit trail
Every business event is a **source document** that *generates* a voucher (rather than someone hand-writing journal entries). Documents can carry attachments (invoice scans) and record who did what and when. This audit chain is the foundation of a production-grade, trustworthy ledger.

---

## 8. Recommended Growth Sequence

Build the smallest closed loop first, then widen — tailored to the project's real operations. **The whole Basic tier ships before any Pro work begins.**

```
Kernel (Phase 0)
   → 🟢 PERSONAL LEDGER  = BASIC TIER   (see where personal money goes)  ← ships first
   ─────────────────────────────────────────────────────────────────────
   → 🔵 Accounting core                 (chart of accounts, double-entry)
   → 🔵 Expenditure + Payroll piece-rate (pay the annotators)
   → 🔵 Revenue / Invoicing              (collect from clients)
   → 🔵 Bank & Cash reconciliation       (reconcile cash)
   → 🔵 Cost / Profit                    (see if it's profitable)
   → 🔵 Fixed Assets
   → 🔵 Tax / AI
```

The first closed loop is the personal one: **record a spend → see it categorised → see it against a budget.** The business loop follows: **pay an annotator → post to the ledger → see it in a report.** Everything else is incremental.

---

## 9. Worked Example: Data-Annotation Piece-Rate Flow

*(🔵 Pro tier.)* This shows the narrow-waist pattern end to end, using the project's real use case. Workers are part-time, modeled as a **service relationship (劳务) paid by piece-rate (计件) on accepted quantity**.

### 9.1 Data model (blueprint)

```
annotator               # the worker
  id, name, id_no, bank_account, entity_id
  relation_type = LABOR_SERVICE        # 劳务 (default) | PART_TIME
  pay_method    = PIECE_RATE           # 计件 | HOURLY | MONTHLY
  agreement_signed, agreement_date, status

project                 # an annotation project, owns its rate
  id, name, entity_id, unit_type        # image / bbox / sentence
  default_unit_price (Decimal), quality_rule

output_record           # the heart of piece-rate
  id, annotator_id, project_id, work_date
  submitted_qty, accepted_qty, rejected_qty
  unit_price (Decimal)                  # SNAPSHOT at time of work
  amount     (Decimal = accepted_qty * unit_price)
  settled (bool), settlement_id (nullable)
  created_by, created_at                # audit

settlement              # one per worker per period
  id, annotator_id, period_start, period_end, entity_id
  gross_amount, tax_withheld, net_amount  (all Decimal)
  status (pending | paid), pay_date, pay_method
  journal_entry_id                      # link to the voucher it posted
```

### 9.2 How it posts to the ledger (the posting rule)

```
On settlement creation (recognize cost):
   Dr  Labor cost / COGS (annotation)        gross
       Cr  Wages payable (劳务报酬应付)        gross

On payment:
   Dr  Wages payable                          gross
       Cr  Bank                               net   (= gross - tax)
       Cr  Tax payable — withheld IIT          tax
```

The annotation spend now flows automatically into **Cost**, **AP**, and the **P&L** — no special-casing in the kernel.

### 9.3 Correctness rules for this flow
1. Pay on **`accepted_qty`** (qualified output), not submitted — ties pay to QA.
2. **Snapshot `unit_price`** on each output record — the same principle as storing the FX rate per transaction; later rate changes never alter history.
3. **`Decimal`** everywhere — unit prices are tiny (e.g. `0.05`), multiplied by huge quantities; `float` would drift.
4. **Idempotent settlement** — once an output record is included in a settlement it is locked (`settled = true`), so it can never be paid twice.

---

## 10. Non-Goals (what "all needs" does *not* mean)

> **"Meet all the needs of a small company" ≠ "build every feature now."**

Trying to build everything up front leads to the never-shipping trap. The objective is the opposite: a core and extension points so well-defined that **adding any future feature is cheap and safe**. Concretely:

- Do **not** gold-plate modules the business does not yet use.
- Do **not** add a feature to the kernel that a subledger could own instead.
- Do **not** let `personal/` and `pro/` reach into each other — shared logic belongs in `core/`.
- Do **not** hold back features behind a paywall; there is no paid tier, and "Pro" is a disclosure boundary, not a commercial one.
- **Do** keep the kernel small, correct, and stable; push variability out to modules and configuration.

---

## 11. Related Documents

- [README](../README.md) — project positioning, the Basic/Pro tier comparison, tech stack, roadmap, and production-grade engineering standards (including the financial-correctness rules this architecture depends on).
