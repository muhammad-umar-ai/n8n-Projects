# Lead Generation Agent through Google Maps

An n8n workflow that collects business leads from Google Maps search results, enriches records with website email addresses, stores lead data in Google Sheets, and generates personalized cold-email drafts for sending through Gmail.

## Workflow overview

1. **Lead Machine form:** Collects business type, target location, requested lead count, and preferred email style.
2. **Google Maps data collection:** Calls the Apify Google Places crawler to retrieve business listings.
3. **Website filter and email extraction:** Keeps records with websites and uses a Gemini-powered Information Extractor to identify an email address.
4. **Lead storage:** Appends business name, website, category, and address to Google Sheets.
5. **Email generation:** Creates a subject and body in the selected style.
6. **Gmail delivery and status tracking:** Sends the generated email and updates the matching Google Sheets row with email and send-time details.

## Requirements

- n8n with the Form Trigger, HTTP Request, Filter, Information Extractor, Google Sheets, Gmail, Wait, and Loop Over Items nodes
- Apify account and Google Places crawler access
- Google Gemini credentials
- Google Sheets OAuth2 credentials
- Gmail OAuth2 credentials

## Setup

1. Import `workflow.json` into your n8n instance.
2. Configure your own Apify actor endpoint and API token. The exported workflow contains a placeholder, not a working token.
3. Connect your Google Gemini credentials to both model nodes.
4. Create a Google Sheet with columns matching the workflow mappings, including Company Name, Category, Website, Phone, Email Address, Address, Cold Mail Status, and SEND Time. Review the exact column names in both Google Sheets nodes.
5. Select your Google Sheet in both Google Sheets nodes and verify the mappings.
6. Connect your Gmail account in the Send a message node.
7. Replace the agency/signature wording in the email-generation prompt with your own business details.
8. Test with a small lead count and verify the extracted email, generated message, sheet updates, and Gmail behavior before enabling the workflow.

## Important review before production

- The workflow sends generated cold emails automatically after import and configuration. Add a human approval step before Gmail if you need to review messages before sending.
- Follow applicable email, privacy, anti-spam, and data-protection requirements. Use legitimate business contact data and provide required sender identification and opt-out handling.
- The current email validation condition only checks whether the extracted value contains `@`; this is not full email validation.
- Confirm that the Google Sheets column names and matching column are consistent. The exported workflow contains different labels in parts of its mappings (for example, Email vs Email Address, and Send Time vs SEND Time).
- The workflow export has not been execution-tested in your n8n instance. Reconnect credentials and verify every node before production use.

## Files

- `workflow.json`: Sanitized n8n workflow export.

