# Telegram Bot for Testing Dobby AI

A simple yet powerful Telegram bot that provides a direct, unfiltered interface for users to test and interact with the `dobby-mini-unhinged-plus-llama-3-1-8b` model from SentientAGI.

This project demonstrates how to quickly set up a public-facing AI chatbot using n8n for the backend logic.

**Bot Link:** [https://t.me/SentientAGIBot](https://t.me/SentientAGIBot)

---

## Features

-   **Direct AI Access:** Users can chat directly with the Dobby AI model without any intermediary filtering or persona layers beyond the system prompt.
-   **Rate Limiting:** To ensure fair use, the bot limits each user to 3 messages per day. Usage is tracked in a Google Sheet.
-   **Open-Source Workflow:** The complete, sanitized n8n workflow is available in this repository for others to learn from and adapt.

## How It Works

1.  **User Message:** The workflow is triggered when a user sends any message to the Telegram bot.
2.  **Rate Limit Check:** The bot looks up the user's Telegram ID in a Google Sheet to check their message count for the current day. If the user is new for the day, they are added to the sheet. If they have exceeded their limit, they are sent a "come back tomorrow" message.
3.  **AI Inference:** If the user is within their limit, their raw message text is sent directly to the Dobby AI model via the Fireworks AI API.
4.  **Telegram Reply:** The AI's response is captured and sent directly back to the user in Telegram.
5.  **Update Count:** The user's `MessageCount` is incremented in the Google Sheet.

## Setup Instructions

To run this workflow yourself:

1.  **Download:** Download the workflow JSON file from this repository.
2.  **Import:** Import the JSON file into your n8n instance.
3.  **Credentials:** Connect your own credentials for:
    *   Telegram
    *   Google Sheets
    *   Fireworks AI (using HTTP Header Auth)
4.  **Google Sheet:** Create a new Google Sheet with three columns: `UserID`, `MessageCount`, and `Date`. Update the Google Sheets nodes in the workflow to point to your new sheet.
5.  **Activate:** Activate the workflow.

## Tech Stack

-   **Automation:** [n8n.io](https://n8n.io/)
-   **AI Model:** SentientAGI's `dobby-mini-unhinged-plus-llama-3-1-8b` via Fireworks AI
-   **Database:** Google Sheets
