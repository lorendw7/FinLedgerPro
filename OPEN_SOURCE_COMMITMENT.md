# Open-Source and Free-Forever Commitment

[English](OPEN_SOURCE_COMMITMENT.md) | [简体中文](OPEN_SOURCE_COMMITMENT.zh-CN.md)

> **Status:** Project governance policy
>
> **Applies to:** The FinLedger Pro public repository, its official releases, and every feature distributed by the upstream project.

---

## Commitment

FinLedger Pro is and will remain a public, free-of-charge, open-source project. The following rules are non-negotiable for the upstream project:

1. **The repository remains public.** Source code, build instructions, documentation, and official release history stay publicly accessible. If the primary host becomes unavailable, the project should be mirrored to another public host.
2. **Official releases remain MIT-licensed.** Every upstream release is distributed under the OSI-approved MIT License. No future release may replace it with a proprietary, source-available, non-commercial, or field-of-use-restricted licence.
3. **No licence fee or paywall.** Basic, Pro, the accounting core, the reference application, and upstream integrations are available without subscription, activation fee, licence key, advertising requirement, or paid feature gate.
4. **No proprietary upstream edition.** The maintainer will not remove a public feature and reserve it for a closed-source or paid FinLedger Pro edition.
5. **No mandatory hosted service.** Core bookkeeping, invoicing, reconciliation, reporting, export, backup, and restore remain usable locally without paying for or signing in to a maintainer-operated service.
6. **Contributions stay open.** Contributions accepted into the public repository are distributed under the repository's MIT License. The project does not require contributors to transfer copyright ownership to the maintainer.
7. **Published rights are preserved.** Release tags and licence notices must not be rewritten to disguise the licence under which a version was originally published.

The legal licence is the unmodified English text in [LICENSE](LICENSE). This governance document records project policy and intent; it does not replace or narrow the MIT License.

---

## Company-Private Extensions

This commitment applies to FinLedger Pro upstream, not to a company's own downstream repository. A company may keep its branding, mappings, workflows, deployment details, and provider-specific extensions private while depending on a tagged public-core release.

That downstream freedom is part of the chosen MIT model. It does not permit the FinLedger Pro maintainer to withhold an upstream paid tier, and it does not require a company to publish confidential business logic or credentials. See [Public Core and Private Company Repositories](docs/public-core-and-private-company-repos.md).

---

## Governance

Any proposal that would make the upstream repository private, charge a licence fee, add a mandatory licence key, create a proprietary upstream feature tier, or replace MIT with a non-open-source licence conflicts with this policy and must be rejected.

Technical safeguards such as protected branches, required reviews, signed commits, and `CODEOWNERS` can reduce accidental or unauthorized changes, but no hosting setting can bind every future administrator forever. The durable protection is the combination of the MIT licence attached to every published version, public release history, public forks and mirrors, and this explicit governance commitment.
