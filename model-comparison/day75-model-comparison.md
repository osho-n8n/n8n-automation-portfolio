# Day 75 — AI Model Comparison: Claude vs OpenAI vs Gemini

## Setup
Built a single n8n workflow ("Day 75 - Model Comparison") with one Chat Trigger feeding three parallel Basic LLM Chain nodes, each connected to a different provider:
- **Claude Haiku 4.5** (Anthropic)
- **OpenAI gpt-4o-mini**
- **Google Gemini (flash-latest)**

One message → three simultaneous responses, compared side by side in n8n's Logs panel.

---

## Test 1 — Basic greeting
**Prompt:** *"Say hello and tell me what AI model you are."*

| Model | Tokens | Speed | Notes |
|---|---|---|---|
| OpenAI | 41 | 11.4s | Misreported itself as "GPT-3.5" despite gpt-4o-mini being configured |
| Gemini | 38 | 1.8s | Correct, concise |
| Claude | 75 | 1.5s | Nearly 2x OpenAI's tokens for the same simple answer |

**Lesson:** Models can misreport their own version internally — trust your own configuration, not the model's self-description.

---

## Test 2 — Conciseness
**Prompt:** *"What are the operating hours of a typical salon? Answer in one sentence."*

| Model | Tokens | Speed |
|---|---|---|
| OpenAI | 50 | 4.8s |
| Gemini | 53 | 2.9s |
| Claude | 72 | 1.7s |

**Result:** All three technically wrote "one sentence" but stuffed it full of clauses instead of giving a short answer.

**Lesson:** Vague brevity instructions ("one sentence," "briefly") don't reliably produce short output. Use explicit constraints instead — e.g., "under 15 words."

---

## Test 3 — Hallucination check
**Prompt:** *"What is the phone number and exact address of Sunset Villa property?"* (never provided as real data)

| Model | Tokens | Speed | Behavior |
|---|---|---|---|
| OpenAI | 63 | 3.0s | Shortest, most direct: "I can't provide that" |
| Gemini | 127 | 16.4s | Added unnecessary padding before asking for more context |
| Claude | 176 | 3.1s | Nearly 3x OpenAI's cost — added an unsolicited bulleted list of alternative search methods |

**Result:** All three passed — no hallucinated phone number or address. All correctly admitted they lacked the data.

**Lesson:** This confirms why giving agents real data-lookup tools (like the Airtable tool in the Real Estate Agentic AI System) matters more than relying on a model to "honestly not know" — cost varies hugely even when all three give the same honest non-answer.

---

## Test 4 — Ambiguous customer scenario
**Prompt:** *"A customer says: 'I want to book but I'm not sure which day works.' What should the assistant do next?"*

| Model | Tokens | Speed | Behavior |
|---|---|---|---|
| OpenAI | 96–108 | 1.7–2.4s | One direct example response |
| Gemini | 292 | 9.3s | Added a full unsolicited mini-strategy + example dialogue with formatting |
| Claude | 250 | 3.8s | Added headers and two separate bulleted lists nobody asked for |

---

## Reliability
Gemini's free tier returned **two separate 503 "Service Unavailable" errors** during testing (Google's own servers under high demand), requiring retries. Claude and OpenAI had **zero failures** across every test.

**Architecture note:** in n8n, when multiple LLM branches run off one trigger, one branch's failure can surface as "Error in workflow" in the chat UI even though other branches succeeded — a real production system would need per-branch error handling so one provider's outage doesn't block the others.

---

## Conclusion

| Model | Best for | Weakness |
|---|---|---|
| **OpenAI (gpt-4o-mini)** | Default choice for structured, cost-sensitive client bots (salon, real estate) — consistently cheapest, fastest to succeed, most disciplined | None significant found today |
| **Claude (Haiku 4.5)** | Fast, high-quality reasoning | Verbose by default — needs explicit "be brief" instructions to control cost |
| **Gemini (flash-latest)** | Free tier, thorough answers when working | Real reliability issues (503 errors) and heaviest token bloat of the three — best as a backup/cost-saving option rather than primary provider |

**Practical takeaway:** OpenAI's gpt-4o-mini remains the safest default for real client automations built during this syllabus. Claude and Gemini are viable alternatives but require tighter prompt constraints to match OpenAI's natural conciseness and cost-efficiency.
