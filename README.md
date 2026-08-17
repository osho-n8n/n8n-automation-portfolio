# n8n Automation Portfolio

Workflow automation projects built in n8n, focused on practical business use cases — lead management, reporting, notifications, and error-resilient system design.

## Projects

### [Capstone 1: Client Lead Capture & Auto-Response System](./capstone-1-lead-capture-system)
An end-to-end automation that captures new client leads from a web form and instantly triggers logging, notification, and response — all in parallel, with zero delay between a lead submitting and the team knowing about it.

### [Capstone 2: Automated Reporting System](./capstone-2-automated-reporting)
A fully automated weekly lead reporting workflow. Pulls new leads, analyzes trends (top lead, hot-lead percentage, busiest day), and delivers a formatted summary to email and Slack every week — with built-in error handling and fallback alerts.

### [Shared Sub-Workflows](./shared-sub-workflows)
Reusable components called across multiple projects:
- **Sub - Send Notification** — priority-based routing (urgent leads get email + Slack, standard leads get Slack only)
- **Sub - Log to Sheets** — generic logging utility for writing structured rows to Google Sheets

## Other Folders
- `airtable-workflows/` — Airtable-specific automation examples
- `email-workflows/` — Gmail-based automation examples
- `error-handling-workflows/` — patterns for resilient, self-recovering workflows
- `practice-workflows/` — training and practice builds
- `rate-limit-handling/` — API rate limit retry logic
- `webhook-security-system/` — layered webhook authentication (token, timestamp/replay, HMAC signature)

## About This Portfolio
These workflows are built as part of ongoing training toward freelance n8n automation consulting for Gulf-region businesses. Each project folder includes its own README with business context, technical details, and setup notes.
