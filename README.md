# Portfolio Resume Request — n8n Automation Workflow

Automated resume delivery system powering [jasherchan.truehubsolutions.com](https://jasherchan.truehubsolutions.com). Triggered by the **Get My Resume** form on the portfolio. Handles deduplication, email delivery, and CRM-style tracking — zero manual effort.

---

## How It Works

```
Visitor fills form
  → Webhook triggers n8n
  → Notion DB checked for duplicate email
  → If new: send resume PDF via Resend + log to Notion
  → If duplicate: silently skip (no double-sends)
```

---

## Stack

| Layer | Tool |
|---|---|
| Trigger | n8n Webhook (POST) |
| Deduplication | Notion Database (email as unique key) |
| Email delivery | Resend (transactional) |
| Resume asset | PDF hosted on Cloudflare Pages |
| Scheduling link | Cal.com (30-min career chat) |
| Automation host | Self-hosted n8n on Hetzner VPS |

---

## Workflow Nodes

1. **Webhook** — Receives `{ name, email, message }` from the portfolio contact form
2. **Notion: Search** — Queries the leads database for the submitted email address
3. **IF: Already exists?** — Branches on whether a matching record was found
4. **Resend: Send Email** — Sends personalised email with resume PDF attachment link and Cal.com scheduling link
5. **Notion: Create Record** — Logs the new lead (name, email, timestamp, source)
6. **No-op (duplicate path)** — Gracefully ignores repeat submissions

---

## Deduplication Logic

Notion acts as the dedup store. Each new submission is checked against a `Email` field (unique per record). If the email already exists, the workflow exits cleanly without sending another email. To reset a specific contact (e.g. for testing), archive or delete the corresponding Notion row.

---

## Environment Variables

All secrets are stored in n8n credentials (never in workflow JSON). The workflow references:

- `NOTION_TOKEN` — Internal Integration Token with write access to the leads DB
- `RESEND_API_KEY` — Resend API key for transactional email
- `RESUME_PDF_URL` — Public Cloudflare Pages URL for the resume PDF
- `CAL_BOOKING_URL` — Cal.com link for the 30-min career chat

---

## Triggering the Webhook

```bash
curl -X POST https://automate.truehubsolutions.com/webhook/resume-request \
  -H 'Content-Type: application/json' \
  -d '{"name": "Test User", "email": "test@example.com", "message": "Test run"}'
```

---

## Workflow Export

See [`workflow.json`](workflow.json) — sanitized export with all credentials removed. Import directly into any n8n instance and re-wire your own credentials.

---

## Related

- Portfolio site: [jasherchan.truehubsolutions.com](https://jasherchan.truehubsolutions.com)
- Built with: Next.js 16 + Tailwind v4 + Cloudflare Pages
- Automation host: Self-hosted n8n on Hetzner VPS (Ubuntu, Docker)
