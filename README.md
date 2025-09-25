# Inbound Voice Agent

This project demonstrates an inbound sales agent for a realestate developer built with Retell.ai, Twilio, and OpenAI GPT-5 mini. The agent qualifies callers, creates bookings, and logs structured JSON outputs directly into Google Sheets.

---

## Stack & LLMs
- **Telephony**: Twilio (SIP trunking, call routing).
- **Voice Runtime**: Retell.ai (handles STT, TTS, real-time inference, transcripts & recordings).
- **LLM**: OpenAI GPT-5 mini (low latency, more cost-effective than GPT-4.1 mini).
- **Automation**: N8N workflows (webhooks, Data logging & transformation in Google Sheets).
- **Storage / Logs**:
  - Retell.ai - transcripts + call recordings.
  - Google Sheets - Raw JSON & Structured JSON outputs for each call.

---

## 🧭 Prompt / Flow Design
**System Prompt**:  
Prompts built with core Human & Machine interation priniciples (RACI).
> You are a polite real estate sales assistant. Greet callers, ask qualifying questions (budget, bedrooms, parking, location, timeframe, finance). Confirm their answers, offer a 15-min booking, then output a JSON object into Google Sheets. Always stay concise and professional.

**Flow:**
1. Greeting & context.
2. Structured Q&A to capture lead details.
3. Confirmation of caller inputs.
4. Book 15-min appointment (Calendly or mock API).
5. Output structured JSON to Google Sheets.
6. Close with a polite summary or escalate to human.

---

## Grounding Approach
- **JSON-first design**  all structured outputs logged in Google Sheets.
- **Dynamic grounding** booking link, office hours, or other context injected dynamically through knowledge pack.
- **Session isolation** each call is stateless (no cross-call memory).

---

## Guardrails
- JSON-only outputs enforced in final step.
- Out-of-scope requests -> default fallback: *“Let me connect you with a team member.”*
- Max ~200 tokens per turn (latency guard).
- Naturalisation of phone numbers, dollar amounts and abbreviations.
- Instructions against providing financial, tax, or legal advice.
- Retell + OpenAI moderation filters active.
- + more guardrails from knowledge pack.

---

## Logging
- **Retell.ai** - transcripts + audio recordings.
- **Google Sheets** - structured JSON records (one row per call).
- **N8N** - Slack alerts if booking or logging fails.

---

## Cost to Run 100 Calls
Assuming 5 min/call (~500 total minutes):

- Twilio: $0.0109/min × 500 = **$5.49**
- Retell.ai(GPT 5 mini): $0.012/min × 500 = **$6.00**
- Misc/storage: negligible

**Total ≈ ~$12 for 100 calls**

---

## What to Improve Next
- CRM integrations (HubSpot, Salesforce) for personalized conversations.
- Dynamic grounding with multiple live property listings, multi- calender.
- Analytics dashboard (conversion, drop-off rates).
- Branded/custom TTS voices.
- Connect a database under an LLM layer to query in natural language.
- Explore open-weight models for cheaper inference.

---

