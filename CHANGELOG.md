# Changelog

[English](CHANGELOG.md) | [简体中文](CHANGELOG.zh-CN.md)

All notable changes to FinLedger Pro are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

Design and documentation phase. No application code has been written yet —
the repository currently holds the project definition, architecture, and licence.

### Added
- Reproducible development baseline for the installed toolchain: Node 24.14,
  pnpm 11.9, CPython 3.13, uv, workspace metadata, safe environment template,
  line-ending/editor rules, and generated JavaScript and Python lockfiles.
- Paired development setup guides covering frozen installs, the uv-managed
  virtual environment, deferred optional tools, and secrets handling.
- Project README defining positioning, scope, technical architecture, and
  production-grade engineering standards.
- Two free feature tiers: **Basic** (personal bookkeeping) and
  **Pro** (business double-entry accounting, opt-in toggle). Both are free and
  MIT-licensed — "Pro" denotes progressive disclosure, not a paywall.
- `docs/architecture.md` — narrow-waist architecture ADR: a small stable
  accounting kernel with `personal/` and `pro/` as feature layers above it, plus
  five extensibility design points and a growth sequence.
- `docs/architecture-narrow-waist.svg` — architecture diagram showing both tiers
  over the shared kernel and the no-cross-dependency boundary between them.
- `docs/xero-product-benchmark.md` — official-source review of Xero's connected
  bookkeeping workflows, product lessons to adapt, capabilities to defer, and
  productivity/reliability requirements for FinLedger Pro.
- `docs/product-roadmap.md` — quality-gated milestones, accounting lessons,
  acceptance gates, release labels, and a parallel shadow-book adoption plan.
- Paired Simplified Chinese editions for the README, architecture, roadmap,
  Xero benchmark, and contribution guide, plus a bilingual docs index.
- `docs/open-api-and-multi-currency.md` and its Chinese edition — replaceable
  provider adapters, ISO 4217 data model, offline fallback, and FX accounting.
- `docs/public-core-and-private-company-repos.md` and its Chinese edition —
  one-way dependency from company-private repositories to tagged public-core
  releases, extension contracts, read-only banking, and secrets boundaries.
- `OPEN_SOURCE_COMMITMENT.md` and its Chinese edition — permanent upstream
  policy covering public visibility, MIT licensing, zero licence fees, local
  usability, contribution licensing, and the ban on a proprietary paid tier.
- Personal ledger design: `PERSONAL` / `BUSINESS` book separation (entity
  assumption), three transaction kinds with `TRANSFER` excluded from spending,
  credit cards as liability accounts, budgets, need-vs-want tagging, and
  recurring-charge detection.
- Payroll design covering Singapore CPF, China 五险一金, three employment
  relationship types, and piece-rate (计件) settlement for data-annotation work.
- Financial-correctness rules (`Decimal` money, balanced entries, derived
  balances, per-transaction FX snapshots, immutable audit trail).
- Companion finance learning path paired with implementation milestones.
- `.gitignore` protecting ledger databases, backups, exports, and secrets.
- `CONTRIBUTING.md` explaining the teaching-project workflow.
- This changelog.

### Changed
- Relicensed from GPL-3.0 to the **MIT License** to keep adoption frictionless
  and leave commercial reuse open.
- Replaced the seven-week feature schedule with quality-gated milestones. The
  first production target is now a complete annotation-settlement and bank-
  reconciliation loop, followed by revenue, month-end close, dual-currency,
  production hardening, and only then optional AI.
- Raised bank reconciliation, period locking, idempotency, duplicate-safe
  imports, and verified restore to first-class production requirements.
- Changed the documentation policy from English-only to paired English and
  Simplified Chinese reader-facing documents; code comments remain English.
- Documented that the maintainer has no commercialisation plan while retaining
  MIT's permissive commercial-use rights for third parties.
- Expanded currency scope from an SGD/CNY-specific API call to an ISO 4217
  multi-currency model with SGD/CNY acceptance first, open-source/self-hostable
  provider candidates, manual rates, provenance, caching, and offline fallback.
- Defined banking integrations as read-only account, balance, and transaction
  feeds. Payment initiation, payouts, beneficiaries, collections, refunds, and
  card control are outside the product scope; externally executed settlements
  are imported and reconciled as accounting evidence.

---

<!--
Release entries will follow this shape once versions ship:

## [0.1.0] - YYYY-MM-DD
### Added
### Changed
### Fixed
### Removed
-->
