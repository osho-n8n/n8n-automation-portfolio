# AI Message Triage Suite

Three-part n8n automation suite that processes incoming customer messages using OpenAI (gpt-4o-mini):

1. **Customer Message Summarizer** — condenses long, messy customer messages into a clear 1-2 sentence summary.
2. **Message Category Classifier** — sorts incoming messages into one of four categories: Maintenance, Payment, General Inquiry, or Complaint.
3. **Message Sentiment Analyzer** — labels each message as Positive, Neutral, or Negative.

## Use case
Designed for businesses (e.g. property management, customer support teams) that receive high volumes of unstructured customer messages via email, forms, or chat, and need fast, automated triage before human follow-up.

## Tech
- n8n workflow automation
- OpenAI gpt-4o-mini via the "Message a Model" node
- Each workflow is a standalone, independently testable unit