# 🚀 AI Prompt Generator

An n8n workflow that turns an initial idea into a structured, ready-to-use AI prompt through a guided multi-step form.

Built by **Muhammad Umar** | [Portfolio](https://umardev.ai.studio) | [Xetomation](https://xetomation.si)

## What it does

1. Collects the user's goal, available tools, expected inputs, and desired output.
2. Uses Google Gemini to generate up to three relevant follow-up questions.
3. Collects answers through dynamic n8n forms.
4. Combines the initial requirements and clarifications.
5. Generates a structured prompt with Role, Inputs, Tools, Instructions, Constraints, and Conclusions.
6. Displays the final prompt so the user can copy and use it.

## Workflow overview

`Form Submission → Basic Questions → AI Follow-up Questions → Dynamic Forms → Merge User Intent → Prompt Generator → Final Prompt`

## Requirements

- An n8n instance with Form Trigger and Form nodes available
- Google Gemini API credentials
- The LangChain nodes used by the workflow

## Setup

1. Import the workflow JSON into n8n.
2. Open both Google Gemini Chat Model nodes and select your own Google Gemini credentials.
3. Review the form pages and prompt instructions for your use case.
4. Test with sample input before sharing the form.
5. Activate the workflow only after verifying the complete flow.

> **Security note:** Never publish API keys, access tokens, or exported credential secrets. Configure your own credentials in n8n after importing.

## Important notes

- The exported workflow is intended as a starting point. Node availability and model settings may vary by n8n version.
- This repository documentation does not imply that a live hosted form is available.
- The workflow should be tested in your own n8n instance before production use.

## About the creator

**Muhammad Umar** is an AI Automation Developer focused on n8n, AI agents, GoHighLevel CRM automation, Python, API integrations, and web scraping.

- 🌐 [Portfolio](https://umardev.ai.studio)
- 🏢 [Xetomation.si](https://xetomation.si)
- 💼 [LinkedIn](https://www.linkedin.com/in/muhammad-umar-56a447257)
- 🎯 [Upwork](https://www.upwork.com/freelancers/~01620156f29b23324e)
- 🟢 [Fiverr](https://www.fiverr.com/sellers/muhammadumar852)

---
Made with n8n and Google Gemini.
