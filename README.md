# N8N_Workflows

This repository serves as a centralized collection of custom n8n automation workflows that I am actively creating and managing[cite: 2]. 

## 📂 Repository Structure

Each directory in this repository represents an independent n8n automation project (such as the `HR Recruitment Workflow`)[https://github.com/shaafkhan10k/N8N_Workflows/tree/main/HR%20Recruitment%20Workflow]. Inside each project folder, you will find:

*   **Workflow JSON:** The exported `.json` file, which contains the complete node architecture and configurations.
*   **Project README:** A dedicated `README.md` detailing the specific logic, API integrations, required credentials, and setup instructions for that individual workflow.

## 🚀 How to Use These Workflows

To deploy any of the automations found in this repository into your own environment:

1.  Clone this repository or download the `.json` file for the specific workflow you want to use.
2.  Open your n8n workspace and create a new workflow.
3.  Click the **menu icon** (three dots) in the top right corner and select **Import from File**.
4.  Upload the target `.json` file.
5.  Update the node configurations by adding your own API keys, OAuth tokens, and platform credentials as outlined in that workflow's dedicated documentation.
6.  Activate the workflow.

## 📝 License

This project is licensed under the MIT License[cite: 2]. See the `LICENSE` file for details.
