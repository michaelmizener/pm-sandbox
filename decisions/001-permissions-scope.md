# Decision Record 001: Scope of Permissions v1

**Date:** 2026-05-10  
**Status:** Accepted  
**Deciders:** Michael (PM), Sarah (Design), Dev Lead

---

## Context

We debated whether to build a full RBAC system (custom roles, fine-grained permissions) vs. a simple 3-tier role model for the initial release.

## Decision

Ship the **3-tier model** (Viewer / Editor / Admin) in Q2. Defer custom roles to v2.

## Rationale

- Custom roles would add 3–4 weeks of eng work and significant design complexity.
- 85% of customer requests can be satisfied with the 3-tier model.
- Shipping faster unblocks expansion in 6 named accounts before Q3 renewal.

## Consequences

- Some power users will ask for more granularity — we'll track this as a signal for v2.
- We accept the risk that the data model will need migration when custom roles ship.
