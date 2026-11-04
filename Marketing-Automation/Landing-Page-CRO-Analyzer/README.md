# Landing Page CRO Analyzer with Google Gemini

An n8n workflow that accepts a landing-page URL, fetches its page content, asks a Gemini-powered AI agent to critique the page and generate 10 tailored conversion-rate-optimization recommendations, then emails the analysis.

## Workflow

1. **Landing Page URL** — n8n Form Trigger collects the target URL.
2. **Scrape Website** — HTTP Request fetches the page response.
3. **AI Agent** — analyzes the returned page content and produces a friendly critique plus exactly 10 actionable CRO recommendations.
4. **Google Gemini Chat Model** — provides the language model for the AI Agent.
5. **Send a message** — emails the generated analysis.

## Requirements

- n8n with Form Trigger, HTTP Request, AI Agent, Google Gemini Chat Model, and Gmail nodes available.
- Google Gemini API credentials.
- Gmail OAuth2 credentials.
- A publicly accessible landing page URL for the HTTP Request node to fetch.

## Setup

1. Import `workflow.json` into n8n.
2. Open **Google Gemini Chat Model** and connect your own Gemini credentials.
3. Open **Send a message** and connect Gmail OAuth2.
4. Replace `YOUR_EMAIL@example.com` with the intended recipient email.
5. Review the **Scrape Website** node's response. Some sites block automated requests, render content client-side, or return incomplete HTML. This starter workflow does not include a dedicated browser-rendering scraper or HTML-to-text extraction layer.
6. Submit a test landing-page URL through the form and inspect the AI Agent output before enabling email delivery.
7. Keep the workflow inactive until credentials and test results are verified.

## Limitations and safety

- The HTTP Request node fetches the URL response; it does not guarantee a complete rendered-page capture. JavaScript-heavy sites may need a browser-based scraper.
- The AI can only analyze content that reaches its prompt. It cannot reliably infer actual conversion rates, analytics, heatmaps, or visitor behavior from page HTML alone.
- The workflow does not validate submitted URLs against private, localhost, or internal network destinations. If exposed publicly, add URL validation and SSRF protections before production use.
- Email recipient is a placeholder. No credential IDs, account names, or personal recipient addresses are included in this export.
- Workflow is inactive by default and has not been live-execution tested in this repository.

## Files

- [workflow.json](./workflow.json) — cleaned n8n workflow export.
