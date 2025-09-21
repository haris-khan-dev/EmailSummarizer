# 📧 Smart Email Auto-Responder (n8n Workflow)

This project is an **automated email summarizer and responder** built with [n8n](https://n8n.io).  
It connects to Gmail, classifies incoming emails, and automatically replies with the appropriate response (project updates, feedback acknowledgments, or scheduling replies). It also integrates with **Google Calendar** to propose meeting times.

---

## 🚀 Features

- **Gmail Trigger**: Fetches incoming emails from a specified Gmail label.
- **AI-Powered Classification**: Uses Google Gemini (via LangChain) to categorize emails into:
  - `Questions` → Meeting scheduling with Google Calendar
  - `Project Updates` → Sends acknowledgement with next steps
  - `Feedback` → Sends thank-you response with tracking ID
- **Automated Responses**:
  - **Questions** → Offers 3 available meeting slots (Google Calendar integration)
  - **Project Updates** → Sends acknowledgment email with next steps
  - **Feedback** → Sends personalized thank-you email with reference ID
- **Post-Processing**:
  - Marks emails as **read**
  - Applies Gmail labels (`CATEGORY_UPDATES`, etc.)
- **Custom Templates**: HTML-based emails with professional formatting.

---

## 🛠️ Tech Stack

- **[n8n](https://n8n.io/)** – Workflow automation platform
- **Gmail API** – For email triggers and label management
- **Google Gemini 2.0 Flash (LangChain)** – For text classification
- **Google Calendar API** – For meeting scheduling
- **SMTP** – For sending automated responses

---

## 📂 Workflow Overview

```mermaid
flowchart TD
    A[Gmail Trigger] --> B{Emails from Existing Contracts?}
    B -->|Yes| C[Skip/Custom Handling]
    B -->|No| D[Reply Filter: Not Re:]
    D --> E[Text Classifier]
    E -->|Questions| F[Google Calendar → Slots → Reply with Invites]
    E -->|Project Update| G[Send Update Acknowledgement Email]
    E -->|Feedback| H[Send Thank You Email]
    F --> I[Mark as Read → Apply Label]
    G --> I
    H --> I
