# FinLedger Pro — Product and Learning Roadmap

> **Status:** Active plan
>
> **Planning model:** Quality-gated milestones, not a calendar promise
>
> **Owner:** The author writes all application code personally. Teaching and discussion are bilingual; repository documentation and code comments are English.

---

## 1. Planning Principles

1. **Real books before broad features.** The first business release must support one complete, reconcilable workflow used by the owner's company.
2. **Trust before automation.** Auditability, reversal, backup, and reconciliation arrive before AI posting or convenience integrations.
3. **Release gates, not week numbers.** A milestone is complete only when its acceptance and recovery tests pass.
4. **Source documents drive accounting.** Bills, invoices, settlements, receipts, and payments generate journal entries through posting rules.
5. **Manual review remains authoritative.** Rules and AI may suggest; the owner approves financial mutations.
6. **Accounting learning accompanies implementation.** Each milestone begins with the relevant finance lesson and ends with a bookkeeping exercise using fabricated data.

The earlier seven-week outline is retired. It was useful for sequencing topics but is not a safe promise for a production accounting release developed by one person.

---

## 2. Milestone Plan

### M0 — Product Definition and Benchmark (complete)

**Learn:** bookkeeping cycles, product scope, and why reconciliation matters.

**Deliver:**

- Product positioning, Basic / Pro boundaries, and local-first constraints.
- Narrow-waist architecture and Xero product benchmark.
- Financial-correctness rules and production release gates.
- MIT licence, contribution policy, and changelog.

**Exit gate:** the documents agree on scope, terminology, build order, and non-goals.

### M1 — Trustworthy Local Foundation

**Learn:** accounting entity assumption, money representation, source documents, and audit evidence.

**Deliver:**

- Electron, React, FastAPI, and SQLite walking skeleton.
- Separate `PERSONAL` and `BUSINESS` books.
- `Decimal` money, currency metadata, dates, time zones, and identifiers.
- Versioned database migrations.
- Append-only audit events and structured local logs without financial values.
- Automatic rotating backups, restore flow, and startup integrity check.
- One personal transaction and one business source document flowing end to end.

**Exit gate:** a forced crash cannot leave a partial transaction; a backup can restore into a clean installation; the same mutation retried twice has one financial effect.

### M2 — Accounting Kernel and Opening Books

**Learn:** five accounting elements, debit / credit rules, accrual accounting, trial balance, and opening balances.

**Deliver:**

- Chart of accounts with account types and report mappings.
- Journal entries and lines, balanced-posting validation, and ACID posting.
- `DRAFT → APPROVED → POSTED → REVERSED` lifecycle.
- Trial balance and general-ledger drill-down.
- Conversion date and controlled opening-balance import.
- Accounting period and lock-date controls.

**Exit gate:** property tests prove that posted entries balance; posted history cannot be edited in place; trial balance reproduces the journal; closed periods reject changes.

### M3 — Spend-to-Reconcile and Annotation Settlement

**Learn:** expenses versus assets, accounts payable, cost recognition, withholding, project costing, and bank reconciliation.

**Deliver:**

- Contacts with customer, supplier, and contractor roles.
- Bills, direct expenses, attachments, due dates, AP aging, and payment status.
- Data-annotation projects, output records, QA acceptance, versioned piece rates, contractor settlements, and project cost allocation.
- Bank accounts and CSV / OFX / QIF statement import into a staging area.
- Import fingerprinting, duplicate detection, manual matching, split transactions, transfers, and reconciliation summary.
- Action Center for unreconciled lines, bills due, settlements pending, and backup health.

**Exit gate:** the real workflow “accepted output → settlement → payable → payment → reconciliation → cost report” completes without a spreadsheet; duplicate import and duplicate settlement tests pass.

### M4 — Earn-to-Reconcile

**Learn:** revenue recognition, accounts receivable, credit notes, deposits, partial payments, and bad-debt handling.

**Deliver:**

- Customer contracts / projects, quotes where useful, invoices, credit notes, and receipts.
- Payment terms, partial payments, invoice reminders, and AR aging.
- Cash and accrual treatment kept separate.
- Bank matching for customer receipts.
- Project revenue, cost, work in progress where needed, and gross margin.

**Exit gate:** “client job → invoice → receivable → receipt → reconciliation → project margin” completes and handles cancellation, partial payment, and overpayment without editing posted history.

### M5 — Month-End Close and Financial Statements

**Learn:** adjusting entries, accruals, prepayments, depreciation, closing, and the relationship between the three statements.

**Deliver:**

- Month-end checklist: reconcile accounts, review AR/AP, post accruals, review anomalies, run reports, back up, and lock the period.
- P&L, Balance Sheet, Cash Flow Statement, AR aging, AP aging, and reconciliation report.
- Drill-down from every report line to journal entries and source documents.
- Comparative periods, budget variance, project / cost-center filters, Excel and PDF exports.
- Fixed-asset register and straight-line depreciation; advanced methods may follow later.

**Exit gate:** an accountant can trace each statement balance to source evidence; balance sheet and cash reconciliation invariants pass; a closed month is reproducible after restore.

### M6 — Dual Currency and Multi-Entity

**Learn:** functional versus transaction currency, realized and unrealized FX differences, intercompany balances, and consolidation.

**Deliver:**

- SGD and CNY transactions with per-transaction FX-rate snapshots and provenance.
- Explicit rounding policy and realized / unrealized FX treatment.
- Entity-isolated books for Singapore and China.
- Intercompany accounts, elimination entries, and consolidated reporting.
- Local tax and statutory settings are effective-dated configuration, not hard-coded constants.

**Exit gate:** historical reports do not change when rates are refreshed; entity data never leaks into another ledger; consolidation balances after elimination.

### M7 — Basic Personal-Finance Completion

**Learn:** cash budgeting, net worth, credit-card liabilities, transfers, and savings rate.

**Deliver:**

- Fast personal income / expense / transfer capture.
- Accounts, hierarchical categories, budgets, alerts, need / want tagging, recurring-charge detection, and CSV export.
- Credit-card purchases treated as expenses and card repayments treated as transfers.
- Personal net-worth and spending reports, strictly isolated from business books.

**Exit gate:** transfers never affect spending; account and net-worth balances derive from transaction history; personal and business books cannot be consolidated.

### M8 — Production Hardening and Release Candidate

**Learn:** threat modeling, recovery objectives, software supply-chain risk, release management, and operational support.

**Deliver:**

- Encryption at rest, OS keychain integration, auto-lock, and safe passphrase recovery guidance.
- Dependency pinning and vulnerability scanning.
- Full unit, property, integration, end-to-end, migration, import, crash, and restore test suites.
- Diagnostics export with no financial data.
- Signed installers, reproducible builds, semantic versioning, upgrade and rollback runbooks.
- Migration test matrix covering every supported release path.

**Exit gate:** the complete production-readiness checklist passes on every supported OS; a release candidate runs for at least one full bookkeeping cycle using parallel shadow books before becoming the sole book of record.

### M9 — Optional Intelligence and Integrations

**Learn:** explainable automation, forecasting limitations, retrieval quality, and safe human approval.

**Deliver only after M8:**

- Rule suggestions, anomaly detection, and cash-flow forecasts.
- Local Ollama / LangGraph analysis with evidence links and confidence labels.
- Tax-knowledge RAG with source dates, jurisdiction, and citations; no filing.
- Optional exchange-rate refresh and, only if justified, selected external integrations.

**Exit gate:** disabling AI changes no accounting result; hallucinated or unavailable AI output cannot post, delete, reconcile, or lock records.

---

## 3. Recommended Release Labels

| Release | Meaning |
|---|---|
| `0.1.0` | M1 foundation; learning build, not for sole-record use |
| `0.2.0` | M2 accounting kernel |
| `0.3.0` | M3 first complete business loop |
| `0.4.0` | M4 revenue loop |
| `0.5.0` | M5 month-end and statements; suitable for shadow bookkeeping |
| `0.6.0` | M6 dual-currency / multi-entity |
| `0.7.0` | M7 complete Basic tier |
| `0.9.0-rc` | M8 release candidate |
| `1.0.0` | Production gates passed and parallel shadow-book trial completed |

Version labels describe capability and confidence, not elapsed time.

---

## 4. Safe Adoption for the Owner's Real Books

Do not switch directly from the current bookkeeping method to an unproven build.

1. Use fabricated data through M4.
2. At M5, create a clean business book with a documented conversion date and verified opening balances.
3. Run FinLedger Pro in **parallel shadow mode** with the existing records for at least one complete monthly close.
4. Reconcile bank, AR, AP, tax-control accounts, and the trial balance against the existing records.
5. Have an accountant or qualified bookkeeper review the chart of accounts, opening balances, posting rules, and first close.
6. Promote the software to the primary book only after M8 gates and the parallel comparison pass.
7. Keep exportable, restorable backups and a documented fallback path at all times.

---

## 5. Scope Beyond Version 1.0

Possible later modules include purchase orders, inventory, employee payroll, expense claims, budgets and forecasts, approval workflows, accountant access, bank feeds, and selected payment integrations. They should be added only when a real operating need exists and through the same source-document, posting, reconciliation, and audit contracts.

“Support a small company” means supporting its **core financial operating cycle reliably**. It does not mean replacing HR, CRM, legal case management, tax filing, banking, or a full ERP in version 1.0.

---

## 6. Related Documents

- [README](../README.md) — product positioning and concise project overview.
- [System Architecture](architecture.md) — narrow-waist design and module boundaries.
- [Xero Product Benchmark](xero-product-benchmark.md) — product lessons, adaptation decisions, and reliability requirements.
