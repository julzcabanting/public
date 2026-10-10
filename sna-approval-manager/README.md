# SNA Approval Manager v1

Reusable WordPress plugin concept for Fluent Forms.

## Intended features

- Multiple Fluent Forms workflows
- Conditional routing by field key, operator, and value
- Email to the selected approver with a secure review link
- One-page application review without WordPress login
- Reusable review access until explicitly revoked
- Approve/Decline decisions can be changed; current status reflects the latest confirmed decision
- Audit trail for every decision
- Optional HTML applicant notification templates for Approved and Declined
- Google Sheets row updates keyed by Fluent Forms entry ID

## Development status

This repository contains project documentation only. The downloadable v1 prototype is not yet production-ready and has not been end-to-end tested against a live WordPress/Fluent Forms installation. Do not use it for production submissions until implementation and security testing are complete.

## Security requirements

- Store only hashed high-entropy tokens; do not log raw tokens.
- A review link grants access to the assigned application. Anyone who possesses a forwarded link may act as that approver, so support link revocation and clearly communicate this limitation.
- Use POST plus nonce/CSRF protection for decisions; do not mutate state on GET requests because email scanners may visit links.
- Sanitize and escape all submission data, and restrict fields shown to approvers.
- Update Google Sheets by unique entry ID; authenticate requests and provide retryable sync status.
- Keep secrets out of source control and client-side code.

## Planned folder layout

- `sna-approval-manager.php` - plugin bootstrap
- `includes/` - settings, routing, database, review actions, audit trail, integrations
- `assets/` - admin and review page styles/scripts
- `integrations/google-apps-script/` - optional Apps Script endpoint
- `tests/` - unit and integration tests
