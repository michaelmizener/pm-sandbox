# Changelog

## [1.4.0] — 2026-06-30

### Added
- **Role-based permissions** — Admins can now assign roles to team members: Viewer, Editor, and Admin
  - Viewers have read-only access across all launches
  - Editors can create and edit launches but cannot archive or delete
  - Admins have full access including member management
- **Private launches** — Admins can mark individual launches as private, limiting visibility to invited members only. Non-members see a lock icon in the list but cannot view content
- Unauthenticated users attempting to access a private launch via direct link are redirected to login, then returned to the launch (access still subject to permissions)

### Changed
- Existing users default to the Editor role upon upgrade
- Org owners are automatically assigned the Admin role
- New invitees default to the Viewer role until a role is explicitly assigned

---

## [1.3.0] — 2026-05-01

### Added
- SSO via Okta for enterprise accounts
- Bulk archive for completed launches

### Fixed
- Date picker incorrectly showing past dates as selectable
- CSV export missing `owner` column

---

## [1.2.0] — 2026-04-15

### Added
- CSV export for launch history

### Changed
- Improved loading performance on the dashboard (P95 latency: 1.8s → 0.4s)

---

## [1.1.0] — 2026-03-15

### Added
- Comment threads on launch items
- @mention notifications (in-app only)

### Fixed
- Duplicate launch entries when refreshing mid-save
