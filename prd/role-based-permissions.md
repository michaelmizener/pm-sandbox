# PRD: Role-Based Permissions

**Status:** In Review  
**Author:** Michael Mizener  
**Last updated:** 2026-05-19  
**Target release:** Q2 2026

---

## Problem

Currently all Launchpad users within an org have the same level of access. This creates two pain points:

1. **Accidental edits** — junior team members accidentally archive or modify launches they shouldn't touch.
2. **Sensitive launch visibility** — some launches (M&A-related, unannounced products) should be restricted to a subset of users.

Customer evidence: 6 of our top 20 accounts have requested this in the past 90 days. It is the #1 requested feature in our Q1 NPS survey (mentioned in 34% of written responses).

---

## Goals

- Allow admins to assign roles to users: **Viewer**, **Editor**, **Admin**
- Restrict destructive actions (archive, delete) to Editors and Admins
- Allow Admins to mark specific launches as **private** (visible only to invited members)
- Do not disrupt existing workflows for orgs that don't configure roles

## Non-goals

- Custom/user-defined roles (v2 consideration)
- Row-level security within a launch (e.g., hiding specific checklist items)
- API key scoping — no changes to read-only token access in this release (separate security initiative)

---

## User Stories

**As an Admin, I want to** assign roles to team members so that I can control who can edit or delete launches.

**As a Viewer, I want to** see launches in read-only mode so that I can stay informed without risking accidental changes.

**As an Editor, I want to** be blocked from archiving launches so that I don't accidentally remove something important.

**As an Admin, I want to** mark a launch as private so that only invited collaborators can see it.

---

## Proposed Solution

### Roles

| Role | Can view | Can edit | Can archive/delete | Can manage members | Can mark private |
|---|---|---|---|---|---|
| Viewer | Yes | No | No | No | No |
| Editor | Yes | Yes | No | No | No |
| Admin | Yes | Yes | Yes | Yes | Yes |

### Default behavior

- Existing users default to **Editor** role upon release.
- Org owners automatically become **Admin**.
- New invitees default to **Viewer** until role is set.

### Private launches

- Only Admins can toggle a launch to private.
- Private launches appear in the list with a lock icon.
- Non-invited users see the launch title but not its content.

---

## Open Questions

- [x] Should Editors be able to invite new Viewers? **No — only Admins can invite members.**
- [x] What happens when a private launch is shared via a public link? **The launch requires authentication. Two cases:**
  - **Not logged in:** redirect to login, then return to the launch URL (or show the error message post-auth if access is still denied)
  - **Logged in but no access:** show inline message: "You do not have access to view this page. If you believe you should have access to view this page, please reach out to your Admin."
- [x] How do we handle API access for read-only tokens? **Out of scope — no changes to API access in this release.**

---

## Success Metrics

| Metric | Baseline | Target (90 days post-launch) |
|---|---|---|
| % of orgs with 2+ roles configured | 0% | 40% |
| Support tickets about accidental edits | 8/month | <2/month |
| Feature adoption (private launches used) | 0 | 25+ orgs |

---

## Timeline

Target GA: week of June 23, 2026. **Infra ticket #52 is the critical path — if it slips past June 6, the release date moves.**

| Milestone | Date | Owner | Notes |
|---|---|---|---|
| PRD finalized & eng kickoff | May 23 | Michael | Resolve any remaining eng questions |
| Infra: JWT role claims complete ([INFRA-52](https://launchpad.atlassian.net/browse/INFRA-52)) | June 6 | Infra team | Blocker for all frontend work |
| Frontend permission guards complete | June 11 | Dev team | 3-day estimate; starts after #52 |
| Admin UI complete | June 13 | Dev team | 4-day estimate; can run in parallel with guards |
| QA & bug fix window | June 16–20 | QA + Dev | Internal testing, edge case coverage |
| Staged rollout (beta accounts) | June 23 | Michael + Dev | Roll out to 5 named accounts first |
| GA | June 30 | Michael | Full release to all orgs |

---

## Dependencies

- Auth service must support role claims in JWT tokens — [INFRA-52](https://launchpad.atlassian.net/browse/INFRA-52) — **blocks all frontend work; must be complete by June 6**
- Frontend permission guards (eng estimate: 3 days)
- Admin UI for role management (eng estimate: 4 days)
