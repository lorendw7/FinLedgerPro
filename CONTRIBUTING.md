# Contributing to FinLedger Pro

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

## Fork freely

The project is [MIT-licensed](LICENSE). You are entirely free to fork it, modify
it, redistribute it, or build a commercial product on top of it — no permission
needed, provided you keep the copyright notice. If the workflow above does not
suit you, forking is a first-class option and no offence is taken.

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

- **All documentation is written in English.**
- **All code comments are written in English.**
- Discussion may happen bilingually (Chinese + English), but written artefacts
  in the repository stay in English.
- Money is always `Decimal` — never floating point. See the
  [financial-correctness rules](README.md#financial-correctness-rules-non-negotiable).
- `personal/` and `pro/` may both depend on `core/`, but **never on each other**.

---

## Where to start reading

- [README](README.md) — positioning, tiers, features, roadmap, engineering standards.
- [docs/architecture.md](docs/architecture.md) — the narrow-waist architecture and why the system is shaped this way.
- [CHANGELOG.md](CHANGELOG.md) — what has been decided and built so far.
