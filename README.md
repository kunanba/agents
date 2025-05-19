# This repo is moving to Azure-samples https://github.com/Azure-Samples/ai-agent-samples/tree/main
# Repository Overview

This repository contains two separate projects:

1. **azure_ai_agent_send_email**  
   An Azure AI Agent that sends emails using a custom email service.

2. **sk_agents**  
   A Semantic Kernel (SK) based SQL assistant that queries a PostgreSQL database and retrieves schema information using two custom plugins.

Each project has its own README file with detailed instructions and required libraries.

---

## Directory Structure

```plaintext
├── azure_ai_agent_send_email
│   ├── README.md              # Instructions and requirements for the email agent.
│   ├── email_services.py       # Contains the email sending function.
│   └── agent_notebook.ipynb    # Notebook demonstrating the email agent functionality.
│   
└── sk_agents
    ├── README.md              # Instructions and requirements for the SQL agent.
    ├── sql_agent.ipynb       # Main notebook containing the SQL and schema plugins and agent integration.
    └── requirements.txt   
```

## Folder Details

### 1. azure_ai_agent_send_email

This folder contains the project that demonstrates how to use an Azure AI Agent to send emails using a custom email service.

**Key Features:**
- **Agent Integration:** Uses Azure AI Agent to process user instructions and trigger an email sending function.
- **Custom Email Function:** Integrates a function that sends an email via Azure Communication Services. The function uses a default email template, modifying only the subject when specified.
- **Environment Variables:** Requires environment variables such as `PROJECT_CONNECTION_STRING`, `MODEL_DEPLOYMENT_NAME`, `EMAIL_COMMUNICATION_SERVICES_STRING`, `RECIPIENT_EMAIL`, and `SENDER_EMAIL` to be set.
- **Required Libraries:** 
  - `azure-ai-projects`
  - `azure-identity`
  - `azure-communication-email`
  - `python-dotenv`

**Usage:**
- Open the provided Jupyter Notebook (or Python script) to see the agent in action.
- Follow the README in this folder for setup instructions and how to run the agent.

---

### 2. sk_agents

This folder contains the project that builds a SQL assistant using the Semantic Kernel framework to interact with a PostgreSQL database.

**Key Features:**
- **SQL Query Plugin:** The `QueryPostgresPlugin` executes SQL queries on a PostgreSQL database.
- **Schema Retrieval Plugin:** The `GetSchemaPlugin` retrieves database schema details, such as table names, column names, and data types.
- **Chat Agent:** Combines the plugins within a `ChatCompletionAgent` that processes user input to generate and execute SQL queries.
- **Environment Variables:** Requires variables like `POSTGRES_CONNECTION_STRING`, `GLOBAL_LLM_SERVICE`, and `AZURE_OPENAI_CHAT_DEPLOYMENT_NAME`.
- **Required Libraries:**
  - `psycopg2-binary`
  - `python-dotenv`
  - `semantic-kernel`
  - `azure-identity`
  - `requests`

**Usage:**
- Follow the README in respective folder for detailed setup instructions and library requirements.
