# Gmail Classification AI Agent

An AI agent that classifies incoming Gmail Inbox messages as **Important**, **Interested**, or **Unwanted** and labels them, so the inbox stays easy to sort and clean up.

Built with Google Apps Script and Google Gemini. It runs on its own every 10 minutes and **never deletes, sends, or marks emails as read**.

<!-- Add a screenshot of your labelled inbox here, then remove this comment:
![Inbox with Smart Inbox labels](docs/inbox-screenshot.png)
-->

## Features

- **AI classification:** Gemini reads the sender, subject, and body of each email.
- **Three labels:**
  - `IMPORTANT`: requires action, has a deadline, or concerns a significant matter.
  - `INTERESTED`: relevant and useful, but not urgent.
  - `UNWANTED`: clearly irrelevant spam or promotions.
- **One label per email:** the prompt requires one of the three categories, so there is no "uncertain" bucket.
- **Example results from my inbox:** broker contract notes and bank alerts were labelled Important, market newsletters Interested, and marketing emails Unwanted. These are results, not fixed rules.
- **Automatic Gmail labelling:** applies the matching `Smart Inbox/...` label.
- **Inbox backfill:** processes existing Inbox messages in batches.
- **Automatic processing:** a time-driven Apps Script trigger runs the worker every 10 minutes.
- **Duplicate protection:** skips messages that already have one of the three labels.
- **Progress tracking:** saves backfill progress in Apps Script Properties so it can resume.

## Technology

- Google Apps Script (JavaScript)
- Gmail Advanced Service
- Google Gemini API

## How it works

1. The worker fetches messages from the Gmail Inbox.
2. It extracts the sender, subject, and readable body text.
3. The email content is sent to the Gemini API.
4. Gemini returns a category and a short reason.
5. The agent applies the matching Gmail label.
6. Progress is saved so backfill can continue across runs.

## Gmail labels

```
Smart Inbox/
├── IMPORTANT
├── INTERESTED
└── UNWANTED
```

## Setup

### 1. Create a Google Apps Script project

Open [Google Apps Script](https://script.google.com/), create a project, and copy the contents of `Code.gs` into the editor.

### 2. Enable the Gmail Advanced Service

1. In the editor, open **Services**.
2. Add **Gmail API**.
3. Save the project.

### 3. Add your Gemini API key

1. Get a key from [Google AI Studio](https://aistudio.google.com/).
2. Open **Project Settings** in Apps Script.
3. Add a Script Property:

| Property | Value |
| --- | --- |
| `GEMINI_API_KEY` | Your Gemini API key |

Never publish or commit your API key.

### 4. Launch the agent

Run the `launchGmailAgent` function from the editor and complete Google's authorization.

The launch function checks the API key, creates the labels, starts the inbox backfill if needed, and installs the automatic 10-minute trigger.

## Configuration

These values are at the top of `Code.gs`.

| Setting | Default |
| --- | --- |
| Gemini model | `gemini-3.5-flash-lite` |
| Maximum email body length | 5,000 characters |
| Batch size | 30 messages |
| Gmail page size | 100 messages |
| Worker interval | 10 minutes |

## Safety and privacy

- Does not send emails.
- Does not delete emails.
- Does not mark emails as read or unread.
- Checks for an existing label before processing a message.
- Keeps the Gemini API key in Script Properties, not in the source code.
- Treats email content as untrusted input in the classification prompt.

Email content is sent to the Gemini API for classification. Review Google's API data policies before using this with sensitive email.

## Limitations

- AI classification can occasionally be wrong.
- Every email gets one of the three categories. There is no separate "uncertain" category.
- Processing is in batches and is subject to Google Apps Script quotas.
- Only Inbox messages are processed, not every Gmail folder.

## Project structure

```
.
├── Code.gs
└── README.md
```

## Status

Working and running on my own inbox. Built with the help of AI tools: I designed the rules, tested the results, and improved it over several iterations.

## License

No license has been specified yet. All rights reserved unless a license is added.
