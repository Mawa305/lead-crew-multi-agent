# Lead Crew: Multi-Agent Lead Pipeline

An n8n workflow with three AI agents that research, qualify, and draft outreach emails for HVAC businesses.

## Flow

1. **Webhook** receives company name, website, and city.
2. **Researcher Agent** gathers info using SerpAPI (Google listing, reviews) and an HTTP tool (company website).
3. **Qualifier Agent** scores the lead from 1 to 10 and lists pain points as JSON.
4. **Parse Qualifier Output** converts the agent's text into structured data.
5. **Lead Filter** routes qualified leads (HVAC, score ≥ 6) to outreach. All leads are logged in Google Sheets.
6. **Outreach Agent** writes a short, personalized cold email.
7. **Gmail Draft** saves the email as a draft for human review.

## Required Credentials

- OpenAI API
- SerpAPI
- Google Sheets (OAuth2)
- Gmail (OAuth2)

## Setup

1. In n8n, go to **Import from file** and select `lead-crew-multi-agent.json`.
2. Re-select each credential (OpenAI, SerpAPI, Google Sheets, Gmail).
3. Replace `YOUR_GOOGLE_SHEET_ID` with your sheet ID in both Google Sheets nodes.
4. Create a Google Sheet with these headers:
   `timestamp | company_name | city | is_hvac_lead | score | status | subject`
5. Test with a POST request to the webhook:

```json
{
  "company_name": "Cool Breeze Heating",
  "website": "https://example.com",
  "city": "Lahore"
}
```

## Notes

- The Gmail node creates drafts only. Emails are not sent automatically.
- Built as part of an n8n automation portfolio.
