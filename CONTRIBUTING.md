# Contributing

Thanks for your interest. This is a personal portfolio project — contributions are welcome in the form of bug reports, workflow improvements, or suggestions.

## Reporting issues

Use the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md). Include your n8n version and the specific node where the issue occurs.

## Suggesting improvements

Open a [feature request](.github/ISSUE_TEMPLATE/feature_request.md). The most useful suggestions are:
- Better deduplication strategies
- Additional notification channels (Slack, Telegram)
- Error handling for failed email deliveries
- Rate limiting for the webhook

## Submitting changes

1. Fork the repo
2. Create a branch: `git checkout -b feat/your-improvement`
3. Make your changes to `workflow.json` or documentation
4. Ensure `workflow.json` remains valid JSON (the CI action will catch this)
5. Open a pull request with a clear description of what changed and why

## Important

Do not commit real credentials, API keys, or webhook URLs. All sensitive values must use placeholder syntax: `{{ YOUR_VALUE_HERE }}`.
