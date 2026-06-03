Automated SEO Competitor Research Pipeline
<img width="1845" height="833" alt="image" src="https://github.com/user-attachments/assets/30c8705c-f001-4eab-8054-838ba19dbfd8" />

An end-to-end automated workflow that accelerates SEO strategy by scraping competitor web pages, extracting key structural data, and leveraging Large Language Models (LLMs) to generate comprehensive content briefs.

This pipeline completely eliminates the manual research phase, condensing hours of competitor layout tracking and keyword gap mapping into a ~12-second automated execution loop.

🚀 Architecture Overview
This automation is built on n8n and utilizes a custom orchestration of web scraping, JavaScript data manipulation, and the Groq API for lightning-fast AI inference.

The Execution Flow:
Trigger Interface (When chat message received): The workflow is initiated via a conversational UI, allowing a user to simply drop a competitor's URL into the chat.

Data Parsing (Extract URL): Extracts and sanitizes the target URL from the chat input.

Web Scraping (Scrape Competitor URL): Navigates to the target URL and pulls the raw HTML content.

Data Truncation & Cleaning (Code in JavaScript): Processes the massive raw HTML payload. This step parses specific SEO tags (Page Title, Meta Description, H1/H2/H3 tags, and Body Content) and truncates the string length to guarantee the payload stays well under the LLM's Token Per Minute (TPM) limits.

AI Inference (Groq AI - Generate Brief): Passes the cleaned data structure to the qwen/qwen3-32b model via Groq's API. A highly engineered system prompt instructs the model to analyze the competitor's structure and output a fully formed markdown content brief (Proposed Title, Meta Description, Target Keywords, and Outline).

Data Formatting (Format Output1): Isolates the clean markdown text from the nested JSON API response.

File Generation (Convert json to html file): Converts the raw markdown/text data into a structured .html (or .md) binary file object.

Cloud Delivery (Upload file): Automatically uploads the generated brief directly into a designated Google Drive folder for immediate access by the content strategy team.

🛠️ Tech Stack
Workflow Engine: n8n (Self-hosted)

AI Provider / Model: Groq API / qwen/qwen3-32b

Data Processing: Node.js / Custom JavaScript

Cloud Storage Integration: Google Drive API

💡 Key Engineering Solutions
Bypassing Context Limits: A custom JavaScript node was engineered to slice and parse heavy DOM elements, ensuring the web scraper doesn't overwhelm the LLM's context window or trigger 429 Rate Limit errors.

Zero-Cost Infrastructure: Designed to run entirely on free-tier APIs (Groq) and self-hosted automation infrastructure, keeping operating costs at $0 while delivering enterprise-grade strategy briefs.

Structured Output Engineering: Utilizes strict prompt engineering to force the LLM to return consistent, structured data formats required for programmatic file conversion.

⚙️ Setup & Installation
Import the provided n8n JSON workflow file into your self-hosted n8n instance.

Configure your Groq API Credential as a Header Auth (Authorization: Bearer YOUR_API_KEY).

Authenticate the Google Drive API node using OAuth2.

Open the n8n Chat Trigger window, paste a target URL, and execute the workflow.
