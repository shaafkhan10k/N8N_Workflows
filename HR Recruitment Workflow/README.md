# HR Recruitment Workflow

An automated end-to-end talent acquisition pipeline built using [n8n](https://n8n.io/). This workflow automates candidate ingestion, CV parsing, GitHub portfolio evaluation, AI-based scoring, role-based candidate routing, email digests for hiring managers, offer letter dispatch, and automated voice calling via AI.

---

## 🏗 System Architecture

```
                               ┌───────────────────────────────────┐
                               │       Google Sheets / Drive       │
                               └─────────────────┬─────────────────┘
                                                 │
                                                 ▼
                                ┌─────────────────────────────────┐
                                │     Extract CV & GitHub Data    │
                                └────────────────┬────────────────┘
                                                 │
                                                 ▼
                                ┌─────────────────────────────────┐
                                │    Claude Sonnet 4 AI Scoring   │
                                └────────────────┬────────────────┘
                                                 │
                                                 ▼
                                ┌─────────────────────────────────┐
                                │       Route & Filter Roles      │
                                └────────────────┬────────────────┘
                                                 │
                                                 ▼
                          ┌──────────────────────┴──────────────────────┐
                          ▼                                             ▼
             ┌─────────────────────────┐                   ┌─────────────────────────┐
             │   Top Candidates Digest │                   │  Offer Letter & Vapi    │
             │     (Gmail Node)        │                   │     Voice Calling       │
             └─────────────────────────┘                   └─────────────────────────┘
```

---

## ✨ Features

- **Automated Data Processing**: Pulls candidate entries from a centralized Google Sheet master list and disqualifies candidates not meeting basic criteria (e.g., GPA < 3.0).
- **CV Data Extraction**: Downloads resume documents directly from Google Drive links and extracts plain text for evaluation.
- **GitHub Portfolio Analysis**: Connects to the GitHub API to fetch public repositories, summarize programming languages used, and extract star metrics for top projects.
- **AI-Powered Evaluation**: Uses **Claude 3.5 / Claude Sonnet 4** to analyze candidate data based on a strict rubric:
  - **CV Fit**: 40%
  - **GitHub Signal**: 30%
  - **GPA**: 20%
  - **Presentation & Communication**: 10%
- **Role Routing & Digests**: Automatically categorizes candidates by role (*AI/ML Engineer, Full Stack Web Development, Video Editing, Game Development*) and sends HTML digest emails to the hiring team featuring the top candidates per category.
- **Human-in-the-Loop Approval**: Integrates n8n's Wait / Approval node allowing the hiring team to review candidates before triggering offer letters.
- **Voice Agent Outreach**: Triggers automated voice calls using **Vapi AI** to reach out to candidates and captures call outcome metrics via incoming Webhooks back into Google Sheets.

---

## 🛠 Prerequisites & Required Integrations

To import and run this n8n workflow, you will need active credentials for the following services:

| Integration | Purpose |
| :--- | :--- |
| **Google Sheets OAuth2** | Read master candidate list and append structured scores & call logs |
| **Google Drive OAuth2** | Download candidate CV files for text extraction |
| **GitHub API** | Fetch public repository summaries and language metrics |
| **Anthropic API** | Candidate scoring via Claude model |
| **Gmail OAuth2** | Send role digests, approval requests, and offer emails |
| **Vapi API / Webhook** | Trigger AI calling agent and log conversation outcomes |

---

## 🚀 Setup & Installation

1. **Download Workflow**: Clone this repository or download `HR Recruitment Workflow.json`.
2. **Import into n8n**:
   - Open your n8n instance dashboard.
   - Go to **Workflows** > **Import from File**.
   - Select the `HR Recruitment Workflow.json` file.
3. **Configure Credentials**:
   - Re-link your respective **Google Sheets**, **Google Drive**, **GitHub**, **Anthropic**, **Gmail**, and **HTTP Header Auth (Vapi)** credentials to each corresponding node.
4. **Update Document & Webhook IDs**:
   - Update the `documentId` fields in the Google Sheets nodes to match your Google Sheet file ID.
   - Update your Vapi `assistantId` in the **Call Candidate (Vapi)** HTTP Request node.
   - Configure your external webhook URL in Vapi to point to the **Vapi Call Outcome Webhook** node path.
5. **Activate Workflow**: Save the workflow and switch the status to **Active** (or trigger manually using the `Run HR Screening` trigger node).

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.