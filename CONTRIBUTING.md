# Contributing to FinLedger Pro

[English](CONTRIBUTING.md) | [简体中文](CONTRIBUTING.zh-CN.md)

Thank you for your interest. Please read this page first — this repository has an
unusual workflow, and knowing it up front will save you time.

---

## This is a teaching project

FinLedger Pro is being built as a **structured learning vehicle**. The author is
learning finance and accounting by implementing them, paced alongside a
curriculum where each week of theory maps onto the module being built.

**The author writes all of the application code personally.** That constraint is
the entire point of the project — code contributed by someone else would defeat
it.

### What this means in practice

| Contribution | Welcome? |
|---|---|
| 🐛 Bug reports | **Yes, very much** |
| 💡 Design feedback, architecture critique, accounting corrections | **Yes, very much** |
| 📖 Documentation fixes (typos, unclear wording, broken links) | **Yes** |
| ❓ Questions about the design or the finance concepts | **Yes** |
| 🔧 Pull requests implementing features | **No** — these will be respectfully declined |
| 🔧 Pull requests refactoring application code | **No** — these will be respectfully declined |

If you spot a bug or a mistake in the accounting logic, **please open an issue
describing it** rather than a PR fixing it. Accounting errors in particular are
extremely valuable to report — this software is intended for real bookkeeping,
so correctness matters more than convenience.

---

## Build downstream freely

The project is [MIT-licensed](LICENSE). You are entirely free to modify it,
redistribute it, or build a private or commercial product on top of it — no
permission needed, subject to the licence notice requirements. For company
customisation, prefer a separate private repository that depends on a tagged
public-core release; use a fork only when a required change cannot be expressed
through an extension contract. See [Public Core and Private Company
Repositories](docs/public-core-and-private-company-repos.md).

---

## Reporting bugs

A good report includes:

1. **What you did** — the steps to reproduce.
2. **What you expected** — especially the *accounting* expectation, if relevant.
3. **What happened instead** — including exact numbers where money is involved.
4. **Environment** — OS, application version, and which tier (Basic / Pro).

> ⚠️ **Never attach real financial data.** Reproduce the issue with fabricated
> amounts, or describe the shape of the data without including it. Do not paste
> database files, exports, or screenshots containing real balances.

---

## Reporting a security issue

Do **not** open a public issue for a security vulnerability. Because this
application stores personal and business financial records on the user's own
machine, please report privately via a
[GitHub security advisory](https://github.com/lorendw7/FinLedgerPro/security/advisories/new)
so a fix can be prepared before disclosure.

---

## Project conventions

If you contribute documentation, please follow the conventions the repository
already uses:

- Major reader-facing documents are maintained as paired English and Simplified Chinese files. Update both editions when changing meaning; English is the canonical technical wording if they temporarily differ.
- **All code comments are written in English.**
- Discussion and reader-facing documents may be bilingual; code comments and
  identifiers remain in English.
- Money is always `Decimal` — never floating point. See the
  [financial-correctness rules](README.md#financial-correctness-rules-non-negotiable).
- `personal/` and `pro/` may both depend on `core/`, but **never on each other**.
- Company-private repositories may depend on tagged public-core releases; the
  public core must never depend on private company code.
- Banking providers are read-only. They may expose accounts, balances, and
  transactions, but never payments, payouts, beneficiaries, collections, or
  card control.

---

## Where to start reading

- [README](README.md) · [中文](README.zh-CN.md) — positioning, tiers, features, roadmap, engineering standards.
- [docs/architecture.md](docs/architecture.md) · [中文](docs/architecture.zh-CN.md) — the narrow-waist architecture and why the system is shaped this way.
- [Open API & multi-currency](docs/open-api-and-multi-currency.md) · [中文](docs/open-api-and-multi-currency.zh-CN.md) — provider and FX design.
- [Public core & private company repositories](docs/public-core-and-private-company-repos.md) · [中文](docs/public-core-and-private-company-repos.zh-CN.md) — downstream and banking boundaries.
- [CHANGELOG.md](CHANGELOG.md) — what has been decided and built so far.
