# AI Customer Support Email Automation

An n8n workflow that monitors a Gmail inbox, filters non-actionable messages, uses AI to classify customer inquiries, retrieves approved knowledge from Pinecone, drafts a grounded response, and routes cases for follow-up.

## Workflow overview

- **Email intake:** Gmail Trigger checks for incoming messages.
- **Initial filtering:** An AI agent classifies messages as `PROCESS` or `IGNORE`. Ambiguous messages are intended to be processed for review.
- **Customer support analysis:** A second AI agent classifies the customer intent, urgency, sentiment, and whether human review is required.
- **Knowledge retrieval:** Pinecone is connected as a retrieval tool. The response-generation instructions require answers to be grounded in retrieved company knowledge and use a holding response when information is missing.
- **Email handling:** The workflow replies to customers and applies Gmail labels according to routing branches.
- **Record keeping:** Customer details, query, classification, human-review flag, and response are appended to Google Sheets.
- **Team notifications:** Additional email notifications are configured for selected issue and escalation routes.

## Main technologies

- n8n
- Gmail
- Google Gemini
- LangChain AI Agent nodes
- Pinecone Vector Store
- Google Sheets

## Import and configuration

1. Import `workflow.json` into your n8n instance.
2. Configure Gmail OAuth2 credentials for the Gmail Trigger, reply, label, and notification nodes.
3. Configure Google Gemini credentials for the chat model and embeddings nodes.
4. Configure Pinecone credentials and select your knowledge-base index.
5. Replace `YOUR_GOOGLE_SHEET_ID` with your own Google Sheets document ID and ensure the expected columns exist.
6. Replace `SUPPORT_TEAM_EMAIL@example.com` with the intended support-team mailbox.
7. Replace `YOUR_GMAIL_LABEL_ID` with the appropriate Gmail label IDs.
8. Review every notification recipient, routing branch, and email template before activating the workflow.
9. Test with sample emails covering normal inquiries, spam/automated messages, missing knowledge, billing disputes, and escalation scenarios.

## Important notes

- The exported workflow has **46 nodes** and **42 connection groups**.
- Credential IDs, account-specific spreadsheet identifiers, Gmail label IDs, and the configured notification recipient have been replaced with placeholders for public sharing. Reconnect and configure these values after import.
- The workflow references a specific Google Sheets column schema and Pinecone index configuration. Your resources must match or the relevant nodes must be reconfigured.
- Review the workflow carefully before production use. In particular, verify that the AI output categories match the Switch node conditions, confirm notification recipients, and test the Gmail reply and label operations.
- AI-generated replies should be monitored until the knowledge base, escalation rules, and routing behavior have been validated with real support scenarios.

## Files

- `workflow.json`: Importable n8n workflow export.
