# Open API and Multi-Currency Strategy

[English](open-api-and-multi-currency.md) | [简体中文](open-api-and-multi-currency.zh-CN.md)

> **Status:** Architecture and product policy
>
> **Initial acceptance currencies:** SGD and CNY
>
> **Goal:** support additional currencies and open data providers without making bookkeeping depend on the network or one vendor.

---

## 1. Terminology

An **open API** is publicly documented and can be called according to published terms. An **open-source API implementation** also publishes its server code under an open-source licence and may be self-hosted. These are not the same.

FinLedger Pro prefers, in order:

1. authoritative public data with clear terms;
2. open-source, self-hostable provider implementations;
3. documented public APIs with replaceable adapters;
4. manual import and entry as the mandatory fallback.

No optional API may become a prerequisite for opening the books, entering a transaction, posting, reconciling, closing, reporting, exporting, backing up, or restoring.

---

## 2. Initial Provider Candidates

### Frankfurter

[Frankfurter](https://frankfurter.dev/) is an open-source, keyless exchange-rate API that can be self-hosted. It aggregates rates from institutional sources and exposes current, historical, and time-series endpoints. It is the preferred first adapter because it supports both a public service and a self-hosted path.

### European Central Bank

The [ECB Data API](https://data.ecb.europa.eu/help/getting-data-web-services-sdmx-0) provides official programmatic access to ECB statistical data. ECB reference-rate publications include SGD and CNY, but the ECB states that reference rates are published for information and discourages using them as transaction rates. FinLedger Pro therefore treats ECB data as a traceable reference source, not as an automatically authoritative accounting or tax rate.

### Manual provider

The manual provider is always enabled. The user may enter a bank, contract, statutory, or accountant-approved rate and attach its source. Manual does not mean untraceable: source description, effective date, operator, and reason are required.

No provider is permanently selected until its licence/terms, availability, historical coverage, SGD/CNY behavior, date semantics, precision, and failure modes have been tested.

---

## 3. Provider Boundary

The domain model does not know any vendor-specific response shape. Every adapter normalises its response into one contract:

```text
ExchangeRateQuote
  base_currency          # ISO 4217
  quote_currency         # ISO 4217
  rate                   # Decimal; documented convention
  rate_date              # economic effective date
  retrieved_at           # local retrieval timestamp
  provider_id
  source_url
  rate_type              # reference | market | bank | statutory | manual
  is_stale
  raw_payload_hash       # evidence without storing secrets
```

The canonical convention is:

```text
1 unit of base_currency = rate units of quote_currency
```

Adapters must reverse or triangulate provider data explicitly and test the result. No implicit rate inversion is allowed in business logic.

---

## 4. Currency Model

The schema supports ISO 4217 currencies from the beginning, while production acceptance starts with SGD and CNY. USD and EUR are the next validation targets because they are common contract and pivot currencies.

Every business transaction preserves:

```text
transaction_currency
transaction_amount
functional_currency
functional_amount
exchange_rate
rate_date
provider_id
rate_type
is_manual_override
rounding_policy_version
```

Each business book has exactly one **functional currency**. Reports may additionally choose a **presentation currency**, but changing presentation never rewrites the ledger.

Historical transactions keep their rate snapshot permanently. Refreshing today's rate must never change an earlier invoice, settlement, payment, or report.

---

## 5. Accounting Treatment

The implementation must distinguish:

- **Transaction-date conversion:** record the source document in both transaction and functional currency.
- **Settlement:** compare the functional amount of cash paid/received with the carrying amount and recognise a realized FX gain or loss.
- **Period-end revaluation:** remeasure eligible monetary balances and recognise an unrealized FX gain or loss according to configured policy.
- **Consolidation translation:** translate another entity's statements for presentation and keep translation adjustments separate from operating profit.

All rules are effective-dated and versioned. Tax or statutory exchange rates may differ from reference or bank rates and must be configured separately.

---

## 6. Offline, Cache, and Failure Policy

1. Cache successful quotes locally with provider, date, and evidence metadata.
2. On weekends or holidays, use the latest prior available rate only after marking its actual rate date.
3. Show age and source wherever a rate is selected.
4. Reject malformed, negative, zero, non-`Decimal`, or implausibly discontinuous data for review.
5. Use bounded timeouts and retries with backoff; never block the accounting workflow indefinitely.
6. Fall back to another configured provider, then cached data, then manual entry.
7. Never silently replace a user-approved or posted rate.
8. Keep provider failures out of financial logs when payloads may contain sensitive data.

---

## 7. Read-Only Integrations

The same adapter pattern may support:

- read-only bank accounts, balances, and transaction feeds;
- tax-reference document updates;
- invoice delivery status;
- company/contact reference data;
- export to accountant or statutory formats.

Every integration requires documented authentication, data classification, permissions, rate limits, timeout/retry behavior, idempotency, audit events, offline behavior, and an exit plan. Financial data must not be sent externally merely because an API is available.

Banking is a one-way evidence channel into FinLedger Pro. The provider contract does not include transfer creation, payment approval, beneficiary management, payouts, direct debits, refunds, collections, or card operations. Imported transactions enter a staging area and cannot post directly to the ledger. Company-specific adapters may live in a private downstream repository as defined in [Public Core and Private Company Repositories](public-core-and-private-company-repos.md).

---

## 8. Acceptance Tests

- SGD↔CNY direct or triangulated quotes reproduce known fixtures within the documented precision.
- Inverting a quote and converting back stays within the explicit rounding tolerance.
- A posted transaction never changes after cache refresh or provider switch.
- Offline mode can enter, post, reconcile, close, report, export, back up, and restore.
- Duplicate provider responses do not create duplicate rate records.
- Re-reading the same bank page or transaction does not create a duplicate statement line or journal effect.
- Contract tests prove that bank providers expose no money-movement method.
- Provider outage follows fallback order and shows a clear stale/manual warning.
- Realized and unrealized FX examples reconcile to the general ledger.
- Every displayed converted amount can reveal the rate, source, date, and rounding rule.

---

## 9. Revisit Triggers

Re-evaluate currency design when the company adds a new functional currency, requires a jurisdiction-specific statutory rate, or needs intraday rates. Re-evaluate read-only integration capacity when transaction volume, provider pagination, or always-on synchronization requires a company-operated worker. Do not expand that review into payment initiation; money movement remains outside the FinLedger Pro boundary.
