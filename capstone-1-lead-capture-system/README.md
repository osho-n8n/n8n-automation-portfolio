# Client Lead Capture & Auto-Response System

An end-to-end automation that captures new client leads from a web form and instantly triggers four parallel actions — no manual follow-up needed.

## The Business Problem

Every minute a new lead waits for a response is a minute they might contact a competitor instead. Manually copying lead details into a CRM, sending a welcome email, and notifying the sales team is slow and error-prone. This system automates the entire process the moment a lead submits a form.

## What It Does

When a potential client fills out the lead form, the system automatically:

1. **Logs the lead in Airtable** — structured record for the sales team to manage and update lead status
2. **Appends the lead to Google Sheets** — a simple, shareable tracker for quick reference or reporting
3. **Sends an instant auto-response email** — the lead receives immediate confirmation their inquiry was received
4. **Notifies the team on Slack** — the sales channel gets a real-time alert with the lead's key details, so no one has to check their inbox to know a new lead came in

All four actions happen in parallel and in seconds, so there's zero delay between a lead submitting the form and the business responding.

## Companion Automation: Daily Lead Summary Report

A second, scheduled workflow runs once daily and sends a summary of that day's leads via email and Slack — giving the team a quick daily pulse on lead volume without needing to check the tracker manually.

## Tech Stack

- **n8n** (workflow automation)
- **Airtable** (lead database)
- **Google Sheets** (lead tracker)
- **Gmail** (auto-response email)
- **Slack** (team notifications)

## Files

- `client-lead-capture-auto-response-system.json` — main lead capture workflow
- `daily-lead-summary-report.json` — scheduled daily summary workflow