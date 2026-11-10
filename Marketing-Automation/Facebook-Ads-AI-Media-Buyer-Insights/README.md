# AI Facebook Ads Media Buyer & Google Sheets Insights

This n8n workflow analyzes Facebook Ads performance for e-commerce campaigns. It fetches the last 28 days of ad-level Insights, filters sales campaigns, calculates ad-level and account-level KPIs, asks Google Gemini to classify each creative, and writes raw metrics plus AI recommendations to Google Sheets.

## Workflow components

- Manual trigger
- NocoDB-backed long-lived Facebook token storage and refresh path
- Facebook Graph API v22.0 Insights request at ad level
- Data parsing for spend, impressions, clicks, add-to-carts, checkouts, purchases, and purchase value
- Sales-objective filter
- Ad-creative aggregation and account benchmark calculations
- Google Gemini model with structured output parser
- Google Sheets raw-data append/update and AI-insight update keyed by `ad_id`

## Requirements

- n8n with Code, HTTP Request, IF, Filter, Merge, Aggregate, Sort, Split Out, NocoDB, Google Sheets, and LangChain/Gemini nodes.
- Meta Developer app with appropriate Marketing API permissions and a Facebook Ads account.
- NocoDB project/table to store the long-lived access token and expiry metadata, or replace the token-management branch with a secure credential solution.
- Google Gemini API credentials.
- Google Sheets OAuth credentials and a spreadsheet with columns matching the workflow mappings.

## Configuration

1. Import `workflow.json` into n8n.
2. Configure the NocoDB nodes with your own project/table and credentials, or replace that token-storage section.
3. Configure the Meta App ID and App Secret in the token-exchange HTTP Request node.
4. Set your Facebook Ad Account ID in the Insights endpoint URL.
5. Connect Google Gemini credentials.
6. Configure both Google Sheets nodes with your own spreadsheet and destination tabs. Ensure `ad_id` is present and unique for matching updates.
7. Review the Meta permissions, token expiry handling, date range, field mappings, and output schema.
8. Test with a small account/date range and verify metrics against Meta Ads Manager before enabling.

## Review before production

- The workflow requests `last_28d`, while part of the AI prompt describes a 14-day period. Align the prompt and date window before relying on comparisons.
- The token refresh check only flags tokens that are still valid and expire within three days; an already-expired token may fall through the non-refresh branch. Add explicit expired/missing-token handling.
- The aggregation code groups records by `ad_name`, while sheet updates match by `ad_id`. Duplicate ad names can combine different ads and should be reviewed; grouping by `ad_id` is safer.
- Verify that the Meta API response includes all requested action types for your account and attribution settings.
- AI categories and recommendations are model-generated decision support, not a substitute for checking profitability, attribution, margins, and account context.
- This is an exported template, not a verified production deployment. Credentials, API permissions, NocoDB schema, and live execution have not been tested here.

## Security

The public workflow export must contain no Meta tokens, App Secrets, NocoDB credentials, private database identifiers, Google Sheet IDs, or personal account data. Configure secrets through n8n credentials or a secure secret store.

## File

- `workflow.json` — cleaned n8n workflow export (configure all credentials and IDs before use).
