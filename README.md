# 📧 Inbox Zero AI Agent System

An AI-powered email management system that helps you achieve inbox zero by intelligently filtering, categorizing, and responding to emails. This system uses OpenAI's GPT models to identify important emails, categorize business opportunities, and draft appropriate responses.

![Inbox Zero](https://img.shields.io/badge/Inbox-Zero-green)
![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![OpenAI](https://img.shields.io/badge/AI-OpenAI%20GPT--4-purple)

## 🌟 Features

- **Smart Email Filtering**: Identifies which emails actually require your attention
- **Automated Response Generation**: Drafts personalized responses to important emails
- **Smart Reply System**: Automatically detects threading information to reply to existing email chains correctly
- **Provider Agnostic**: Configured for IMAP/SMTP (Gmail, Outlook, etc.)
- **Spam & Marketing Detection**: Intelligently filters out mass marketing emails from genuine opportunities
- **Interactive Review**: Review, edit, or skip generated responses before sending

## 📋 Components

The system consists of two main components:

1. **Important Email Detector** (`important_email.py`): Analyzes your inbox (via IMAP), identifies emails that truly need your attention, and saves them to a structured JSON file.
2. **Email Response Generator** (`email_responder.py`): Reads the analyzed emails, creates draft responses using AI, and allows you to review and send replies (via SMTP).

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- OpenAI API key
- Email account with IMAP/SMTP access (e.g., Gmail with App Password)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/AllAboutAI-YT/email-agents.git
   cd email-agents
   ```

2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Create a `.env` file with your credentials:
   ```
   OPENAI_API_KEY=your_openai_api_key_here
   EMAIL_USER=your_email@gmail.com
   EMAIL_PASS=your_app_password
   ```

   > **Note:** For Gmail, you must use an [App Password](https://support.google.com/accounts/answer/185833), not your regular login password.

## 🔍 Usage

### Step 1: Find Important Emails

```bash
python important_email.py
```

This will:
- Connect to your email via IMAP
- Fetch emails from the last 24 hours
- Analyze each email for importance using OpenAI
- Check if you've already responded (by checking your Sent folder)
- Save important emails to `needs_response_emails.json` and generate a report in `needs_response_report.txt`

### Step 2: Generate and Send Responses

```bash
python email_responder.py
```

This will:
- Read important emails identified in Step 1
- Draft customized responses for each email using AI
- Present each draft for your review
- Allow you to:
  - **y**: Send the response (replies to the original thread)
  - **n**: Skip this email
  - **edit**: Rewrite the response based on your instructions
  - **skip**: Skip without action

## ⚙️ Configuration

You can adjust the system's behavior by modifying constants in the files:

- **IMAP/SMTP Settings**: In `important_email.py` and `email_responder.py`
  - Default is `imap.gmail.com` and `smtp.gmail.com`
  - Change to `outlook.office365.com` / `smtp.office365.com` for Outlook
- **Time Window**: Change `hours=24` in `important_email.py` to scan a different period
- **AI Model**: The system defaults to `gpt-4.1` (ensure you have access or change to `gpt-4o` / `gpt-3.5-turbo`)

## 📁 Output Files

The system generates several output files:
- `needs_response_emails.json`: Structured data of important emails (used by the responder)
- `needs_response_report.txt`: Human-readable report of emails needing responses
- `recent_emails.txt`: Raw text dump of fetched emails (for debugging)
- `response_history.json`: Log of emails that have been responded to

## 🛡️ Security

- All API keys and passwords are stored in the `.env` file (not in Git)
- The `.gitignore` file should prevent sensitive data from being committed
- **Recommendation**: Use App Passwords instead of main account passwords

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
