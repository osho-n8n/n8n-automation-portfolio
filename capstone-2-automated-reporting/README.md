# Automated Reporting System

A fully automated weekly lead reporting workflow built in n8n. This system removes the need for manual weekly reporting by automatically pulling new leads, analyzing them, and delivering a summary straight to email and Slack — every week, without anyone lifting a finger.

## What It Does

Every Monday at 8:00 AM, the workflow:

1. **Pulls new leads** from the last 7 days out of Airtable
2. **Analyzes the data** — total lead count, top-performing lead, percentage of "Hot" leads, and the busiest day of the week for submissions
3. **Delivers the report** in parallel to:
   - **Email** (Gmail) — a formatted summary for records or forwarding to stakeholders
   - **Slack** — a quick-glance version posted to the team channel

If no new leads came in that week, the system still sends a clear "no leads this week" message rather than an empty or broken report — so there's never any ambiguity about whether the automation ran.

## Business Value

- **Saves hours of manual work** — no one needs to open Airtable, filter by date, and compile numbers by hand every week
- **Consistent, on-time reporting** — the report goes out at the same time every week without relying on someone remembering to do it
- **Surfaces what matters** — automatically highlights the top lead and hottest trends, not just raw data
- **Built-in reliability** — if email or Slack delivery fails, the system logs the failure and sends a backup alert instead of failing silently

## How It Works (Technical Overview)

- **Trigger:** Weekly Schedule Trigger (Mondays, 8:00 AM, Asia/Qatar timezone)
- **Data source:** Airtable, filtered to leads submitted in the last 7 days
- **Processing:** A Code node aggregates the data — lead count, top lead by score, hot-lead percentage, and busiest submission day (with tie-break handling for days with equal activity)
- **Delivery:** Parallel branches send the report to Gmail and Slack simultaneously
- **Error handling:** If either delivery channel fails, the workflow automatically retries via a fallback notification path and logs the error for review — so failures are visible, not silent

## Notes

This workflow is part of a broader automation portfolio and is built to be reusable — the underlying pattern (scheduled pull → aggregate → multi-channel delivery → error handling) can be adapted for other types of recurring reports beyond lead data.
