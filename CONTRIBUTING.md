# Contributing

Thank you for your interest in improving this n8n workflow collection.

## Before contributing

- Do not include API keys, passwords, access tokens, personal data, or private webhook URLs.
- Test workflows in a non-production n8n environment before submitting them.
- Use clear node names and remove unused nodes.
- Include a project README with prerequisites, setup, expected inputs and outputs, and testing steps.

## Suggested project structure

```
Project-Name/
├── README.md
├── workflow.json
├── screenshot.png
└── assets/
```

## Workflow exports

Export workflows as JSON and verify that credential secrets are not included. Reference credentials by a clear placeholder name and explain how users should reconnect their own credentials.

## Pull requests

Describe the workflow's purpose, required services, setup steps, and any known limitations. Include screenshots when they help explain the workflow.
