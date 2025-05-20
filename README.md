# 📬 Knowledge Base Email Workflow (n8n + Airtable + OpenAI + Google Sheets)

This project automates an intelligent knowledge base query system triggered by incoming emails. It integrates IMAP email listening, dynamic context-building from Airtable and Google Drive, OpenAI-powered Q&A, and logging through Google Sheets—all orchestrated using [n8n](https://n8n.io).

---

## 🔁 Workflow Summary

1. **Email Trigger (IMAP)**  
   Listens for new incoming emails via a configured mailbox.

2. **Extract and Clean Query**  
   Parses the email content, removes HTML/signature noise, and extracts a clean user question.

3. **Fetch Airtable Data**  
   Pulls three related datasets:
   - **Camps**
   - **Campers**
   - **Documents**

4. **Merge & Structure Context**  
   Merges the fetched data into a structured context block (JSON) with:
   - Total number of camps/campers
   - Key dates and document types
   - Contextual insight to support LLM-based answers

5. **Generate AI-Powered Answer (OpenAI)**  
   Sends the user’s question and contextual JSON to the GPT-4 model with role-based prompting for concise, direct answers.

6. **Log to Google Sheets**  
   Appends timestamped query, answer, and referenced documents to a connected Google Sheet for audit & review.

7. **Email Response**  
   Sends a clean, formatted reply to the original sender with their AI-generated answer.

---

## ⚙️ Stack

| Tool              | Purpose                                   |
|-------------------|-------------------------------------------|
| **n8n**           | Workflow automation and orchestration     |
| **Airtable**      | Data source for camps, campers, documents |
| **OpenAI API**    | LLM-powered Q&A engine                    |
| **Google Sheets** | Logging historical Q&A pairs              |
| **IMAP**          | Email listener for incoming queries       |
| **SMTP**          | Email sender for replies                  |

---

## 📎 Example Use Case

A parent emails a question like:  
> “When does Camp Horizon start and what documents do I need to bring?”

This system:
- Cleans and extracts that query
- Gathers structured data from Airtable (camp dates, document types)
- Feeds it to GPT-4 for contextual response
- Sends a polished email answer back
- Logs the interaction in Google Sheets for reference

---

## 🛠 Configuration Notes

- Replace all credential placeholders (`baseId`, `imap`, `smtp`, API keys) with your secured values.
- Your Airtable must have the expected fields like `StartDate`, `EndDate`, `Type`, `Content`, and `URL`.
- The Google Sheet must have matching columns: `Timestamp`, `User Query`, `AI Answer`, `Document Names`, `ID`.

---

## 🚀 Future Enhancements

- Add Google Drive API to fetch and embed actual doc previews.
- Use webhooks or cron scheduling to supplement email triggers.
- Introduce multi-language support.
- Integrate a feedback loop for accuracy rating of responses.

---
