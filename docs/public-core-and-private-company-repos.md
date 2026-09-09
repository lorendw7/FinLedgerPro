# Public Core and Private Company Repositories

[English](public-core-and-private-company-repos.md) | [简体中文](public-core-and-private-company-repos.zh-CN.md)

> **Status:** Accepted architecture decision
>
> **Decision:** FinLedger Pro publishes the reusable accounting core and reference application in the public repository. Each company may build a separate private repository that depends on a released version of that public core.

---

## 1. Repository Boundary

The public project is a complete, usable accounting foundation rather than a hosted service or a proprietary paid tier. It contains the general-purpose capabilities that should be shared and tested by everyone:

- books, accounts, `Decimal` money, audit events, migrations, backup, and restore;
- chart of accounts, balanced posting, journal, trial balance, period locks, and financial statements;
- contacts, bills, invoices, credit notes, receivables, payables, receipts, and accounting payment records;
- bank-statement staging, duplicate detection, matching, reconciliation, and read-only bank-feed contracts;
- stable extension contracts, reference adapters, and contract tests.

A company-owned private repository contains only the parts that are specific to that company:

- branding, navigation, and company-specific screens;
- chart-of-account mappings, invoice layouts, approval policy, and operating configuration;
- private workflows and integrations, such as an Aspire read-only transaction adapter;
- deployment configuration and internal operating documentation.

The dependency direction is one-way:

```text
company-private-repository
        │
        │ depends on a tagged public release
        ▼
FinLedger-Pro public core
```

The public core must never import, call, or require company-private code. The recommended model is a versioned dependency, not a long-lived private fork. A private fork is reserved for a temporary core patch that cannot yet be expressed through an extension contract.

---

## 2. Extension Contracts

Private modules may interact with the public core only through published contracts:

- source-document commands create drafts and post through the accounting kernel;
- reports read documented ledger views or query services;
- extensions own their private tables and migrations instead of altering core tables directly;
- bank adapters emit normalized statement records into the public staging area;
- no extension writes journal rows, balances, or reconciliation decisions directly.

Each public release provides contract tests that a company repository runs in CI. Semantic-versioning rules apply to extension interfaces, database migrations, and normalized data models.

---

## 3. Read-Only Banking Scope

FinLedger Pro may read bank data but does not control money movement. The public banking contract is deliberately read-only:

```text
BankFeedProvider
  list_accounts()
  get_account_balance(account_id)
  list_transactions(account_id, cursor, date_range)
  health_check()
```

Provider data follows this path:

```text
bank API or statement file
  → immutable import batch
  → normalized statement lines
  → fingerprint and duplicate checks
  → match suggestion
  → human-confirmed reconciliation
  → accounting record and audit evidence
```

An adapter must preserve the provider transaction ID, status, booking/value timestamps, original amount and currency, direction, reference, pagination cursor, retrieval time, and a safe payload hash. Pending and settled transactions remain distinct. Importing the same page or transaction twice must have one effect.

### Explicitly out of scope

FinLedger Pro will not:

- create or approve bank transfers;
- manage beneficiaries;
- initiate payouts, direct debits, refunds, or payment collection;
- issue or control cards;
- expose payment credentials to the user interface;
- treat a bank API response as a posted journal entry without staging and reconciliation.

The ledger may record that an invoice was paid or a payable was settled. That is an accounting fact observed from an imported bank transaction or entered with evidence; it is not an instruction to the bank.

---

## 4. Secrets and Financial Data

A private Git repository is not a secrets vault. API credentials, tokens, real bank payloads, ledger databases, exports, and backups must never be committed to either repository. Runtime credentials belong in the operating-system keychain or an approved secret manager and should use the narrowest available read-only scope.

Provider-neutral code should normally be contributed to the public core. Company mappings, private workflows, and deployment details remain in the company repository. A generic provider adapter may also be public when its terms allow redistribution and it contains no company data or credentials.

---

## 5. Licensing

The public repository remains MIT-licensed. A company may keep its company-specific repository private and may use the public core in internal or commercial software subject to the MIT notice requirements. This is not a proprietary FinLedger Pro edition: the maintainer does not withhold a paid feature tier, while downstream companies retain ownership and control of their own extensions.
