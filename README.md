Gmail Classification AI Agent

An AI-powered Gmail classification system built with Google Apps Script and Google Gemini.

The agent automatically analyses incoming Inbox messages and organises them into three categories using AI-based email classification.

Features

- AI-powered classification: Uses Google Gemini to analyse email sender, subject, and body.
- Three classification labels:
  - "IMPORTANT" — Emails requiring attention, action, or involving significant matters.
  - "INTERESTED" — Relevant and useful emails that are not urgent.
  - "UNWANTED" — Irrelevant spam and unwanted promotional emails.
- Automatic Gmail labelling: Applies the appropriate Smart Inbox label.
- Initial Inbox backfill: Processes existing Inbox messages in batches.
- Automatic processing: Uses a time-driven Google Apps Script trigger.
- Duplicate protection: Skips messages that already have one of the three classification labels.
- Progress tracking: Stores backfill progress using Google Apps Script Properties.

Technology Stack

- Google Apps Script
- Gmail Advanced Service
- Google Gemini API
- JavaScript

Architecture

1. The worker retrieves messages from the Gmail Inbox.
2. Email sender, subject, and readable body text are extracted.
3. The email content is sent to the Gemini API.
4. Gemini returns a category and a short explanation.
5. The agent applies the corresponding Gmail label.
6. Processing progress is saved so that backfill can continue across executions.

Gmail Labels

The agent uses the following label structure:

Smart Inbox/
├── IMPORTANT
├── INTERESTED
└── UNWANTED

Setup

1. Create a Google Apps Script project

Open "Google Apps Script" (https://script.google.com/) and create a project.

Copy the contents of "Code.gs" into the project editor.

2. Enable Gmail Advanced Service

In the Apps Script editor:

1. Open Services.
2. Add Gmail API.
3. Save the project.

3. Configure the Gemini API key

1. Obtain a Gemini API key from "Google AI Studio" (https://aistudio.google.com/).
2. Open Project Settings in Apps Script.
3. Add a Script Property:

Property| Value
"GEMINI_API_KEY"| Your Gemini API key

Do not publish or commit your API key.

4. Launch the agent

Run the "launchGmailAgent" function from the Apps Script editor and complete Google's authorization process.

The launch function checks the API key, prepares the labels, initializes backfill if necessary, and installs the automatic worker trigger.

Configuration

The main configuration values are defined near the beginning of "Code.gs".

Setting| Default
Gemini model| "gemini-3.5-flash-lite"
Maximum email body length| 5,000 characters
Batch size| 30 messages
Gmail page size| 100 messages
Worker interval| 10 minutes

Safety and Privacy

- The agent does not send emails.
- The agent does not delete emails.
- The agent does not mark emails as read or unread.
- Existing classification labels are checked before processing.
- The Gemini API key is stored in Script Properties rather than in the source code.
- Email content is treated as untrusted input by the classification prompt.

Email content is transmitted to the Gemini API for classification. Review Google's applicable API data policies before using the system with sensitive email information.

Limitations

- Classification is AI-based and may occasionally be incorrect.
- The system applies one of three categories; it does not provide a separate uncertain category.
- The worker processes messages in batches and is subject to Google Apps Script execution and service quotas.
- The current implementation processes Inbox messages, not every folder in Gmail.

Project Structure

Gmail-Classification-Ai-Agent/
├── Code.gs
└── README.md

Project Status

Built using Google Apps Script and Google Gemini.

The repository contains the source code for the Gmail classification agent. Deployment requires configuring the Google Apps Script project, Gmail Advanced Service, and Gemini API key.

License

No license has been specified yet. All rights reserved unless a license is added to this repository.