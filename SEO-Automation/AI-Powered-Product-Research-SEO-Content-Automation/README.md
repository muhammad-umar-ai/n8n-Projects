# AI-Powered Product Research & SEO Content Automation

An n8n workflow that accepts a product title, searches Google Custom Search for competitor pages, extracts titles/snippets/keywords, generates SEO metadata and product copy with a Gemini-powered LangChain chain, then writes structured output to Google Sheets.

## Workflow overview

1. **On form submission** — collect a product title.
2. **Edit Fields** — normalize the title field for the search request.
3. **Google Search** — call the Google Custom Search JSON API for pages matching the product title.
4. **Extract Competitor Data** — collect result titles, snippets, and unique words from titles.
5. **Basic LLM Chain + Google Gemini Chat Model** — generate SEO metadata and a product description.
6. **Code Formatting** — split the generated text into SEO metadata and product-content records.
7. **Google Sheets** — append/update the resulting records.

## Requirements

- n8n with the HTTP Request, Form Trigger, Code, Google Sheets, and LangChain nodes available.
- Google Programmable Search Engine / Custom Search JSON API credentials:
  - API key
  - Search Engine ID (`cx`)
- Google Gemini API credentials.
- Google Sheets credentials and a destination spreadsheet.

## Setup

1. Import `workflow.json` into your n8n instance.
2. In **Google Search**, replace the `your key` and `your cx` placeholders with your own values. Prefer storing the API key in n8n credentials or an environment variable rather than committing a real key.
3. Connect your Google Gemini credentials to **Google Gemini Chat Model**.
4. Configure the spreadsheet and sheet in **Google Sheets**. Confirm the destination columns match the output fields:
   - `type`, `title`, `description`, `keywords`, `product_title`, `product_description`
5. Review the Google Sheets operation and matching-column settings for your spreadsheet.
6. Test with a sample product title and inspect each node's output before activating the workflow.

## Important implementation notes

- The exported workflow is a starter template. Credentials and destination spreadsheet settings are intentionally not supplied.
- The Google Search query focuses on pages with the product title in the page title and excludes selected social/video sites.
- Keyword extraction is a lightweight heuristic based on words in result titles; it is not search-volume or ranking-difficulty research.
- The LLM prompt requests a 120–160 character meta description and a product description of at least 150 words. Generated SEO content still requires factual review.
- The workflow is inactive by default. Live execution has not been verified as part of this repository publication.
- The original workflow's visual sticky-note annotations are omitted from this cleaned export; functional workflow nodes and connections are retained.

## Security

Never commit API keys, access tokens, credentials, private spreadsheet URLs, or customer data. Configure credentials in your own n8n instance.

## Files

- [workflow.json](./workflow.json) — importable n8n workflow export.

