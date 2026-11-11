# Free Powerful Long-Tail Keywords

An n8n SEO keyword research workflow that turns a niche/topic into seed keywords, expands them with Google Autocomplete suggestions, generates long-tail keyword ideas with Gemini, and appends the results to Google Sheets.

## Workflow overview

1. **Chat Trigger** — accepts a niche or topic from the user.
2. **Gemini seed keyword finder** — generates 10 short seed keywords (2–3 words).
3. **JavaScript parser** — parses the model's JSON Lines response into individual items.
4. **Loop + Google Suggest** — iterates over seed keywords and requests Google Autocomplete suggestions.
5. **JavaScript parser** — extracts suggestion strings from the Google Suggest response.
6. **Second loop + Gemini** — generates five long-tail keyword ideas (4–8 words) for each suggestion.
7. **JavaScript parser + Google Sheets** — parses the generated long-tail results and appends rows.
8. **Wait** — pauses for two minutes between loop iterations.

## Requirements

- n8n with the Chat Trigger, Google Gemini, Code, Loop Over Items, HTTP Request, Google Sheets, and Wait nodes.
- A Google Gemini API credential.
- A Google Sheets OAuth2 credential.
- A Google Sheet with these columns:
  - `category`
  - `keywords`
  - `seed keywords`
  - `long-tail keywords`

## Setup

1. Import `workflow.json` into n8n.
2. Add your own Google Gemini credential to both Gemini nodes.
3. Connect your Google Sheets OAuth2 credential to the Google Sheets node.
4. Replace `YOUR_GOOGLE_SHEET_ID` with your spreadsheet ID and select the correct worksheet.
5. Confirm that the sheet headers match the four column names above.
6. Test the workflow with a small niche before enabling or sharing the chat trigger.

## Important validation notes

- The exported workflow has been sanitized: credential references, personal spreadsheet ID, webhook IDs, and instance metadata have been removed or replaced with placeholders. It is inactive by default.
- The Gemini nodes are instructed to return multiple JSON objects on separate lines. The Code nodes parse each line independently; test the actual Gemini response format and add error handling for Markdown fences, malformed JSON, or unexpected output.
- The Google Suggest request currently wraps the keyword in encoded curly braces (`%7B...%7D`). Verify that this produces the intended autocomplete suggestions; remove the braces if they reduce or alter results.
- The second Gemini prompt includes a 2025 example term. Update the prompt's year dynamically or replace it with the current target year when appropriate.
- The workflow writes rows to Google Sheets inside nested loops. Check the item pairing and execution results to ensure each generated long-tail keyword is associated with the intended original niche and seed keyword.
- Add retries/rate-limit handling for Google Suggest and Gemini, and test the two-minute wait against your expected volume and API quotas.

## Security

Do not commit API keys, OAuth tokens, private spreadsheet IDs, or personal data. Reconnect credentials inside your own n8n instance after importing.

## Included file

- `workflow.json` — sanitized n8n workflow export (11 nodes).
