# Changelog

All notable changes to this project are documented here.

## [1.1.0] — 2026-04-26

### Added
- Sanitized `workflow.json` export for easy import into any n8n instance
- Full architecture documentation in README
- Environment variable reference section
- curl test command for local webhook testing

## [1.0.0] — 2026-04-24

### Added
- Initial workflow: webhook trigger → Notion dedup → Resend email delivery → Notion lead logging
- Graceful no-op path for duplicate submissions
- Webhook responds with `{"status": "ok"}` on all paths
