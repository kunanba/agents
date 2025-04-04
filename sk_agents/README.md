# SQL AGENT with PostgreSQL Plugins

This repository demonstrates how to create a SQL query agent that leverages two custom plugins to interact with a PostgreSQL database. The solution uses a semantic kernel framework to build two plugins:

- **QueryPostgresPlugin:** Executes SQL queries on a PostgreSQL database.
- **GetSchemaPlugin:** Retrieves the schema details (tables, columns, and data types) from the database.

These plugins are then integrated into a ChatCompletionAgent that analyzes user requests, retrieves relevant schema information, generates an appropriate SQL query, executes it, and returns the query results.

## Overview

The solution includes:
- **Plugin Classes:**  
  - `QueryPostgresPlugin`: Accepts a SQL query as input and returns the query results.
  - `GetSchemaPlugin`: Queries the `information_schema.columns` view to return table schemas as a formatted string.
- **Agent Integration:**  
  - A `ChatCompletionAgent` that uses the above plugins to answer user requests by retrieving schema information and executing SQL queries.
- **Environment Integration:**  
  - The system loads environment variables (such as PostgreSQL connection string and Azure OpenAI service credentials) from a `.env` file.

## Prerequisites

- **Python 3.9+**
- A PostgreSQL database with a public schema containing tables (e.g., the `actor` table).
- An Azure OpenAI (or similar) service for semantic kernel integration.
- Environment variables set in a `.env` file:
  - `POSTGRES_CONNECTION_STRING`: Your PostgreSQL connection string.
  - `GLOBAL_LLM_SERVICE`: The service ID for your global language model (e.g., Azure OpenAI Chat deployment name).
  - `AZURE_OPENAI_CHAT_DEPLOYMENT_NAME`: The Azure OpenAI Chat deployment name.

## Installation

1. Clone the repository:
    ```bash
    git clone <repository_url>
    cd <repository_directory>
    ```
2. Create a virtual environment and activate it:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```
3. Install required packages:
    ```bash
    pip install -r requirements.txt
    ```

   **Note:** Ensure that your `requirements.txt` includes dependencies such as `psycopg2`, `python-dotenv`, `semantic-kernel` (and its dependencies), and any other packages used in your code.

## Project Structure

```plaintext
├── README.md
├── .env                    # Environment variable definitions
├── sql_agent.ipynb     # Jupyter Notebook version of the solution
└── requirements.txt        # Python package requirements

## Usage

### Running the Notebook

1. **Open the Notebook:**
   - Open `main_notebook.ipynb` in Jupyter Notebook or VS Code.

2. **Set Environment Variables:**
   - Ensure your `.env` file (in the project root) contains the required variables:
     - `POSTGRES_CONNECTION_STRING`
     - `GLOBAL_LLM_SERVICE`
     - `AZURE_OPENAI_CHAT_DEPLOYMENT_NAME`

3. **Execute the Cells:**
   - Run the notebook cells sequentially. The notebook will:
     - Load PostgreSQL and Azure OpenAI credentials.
     - Instantiate the `QueryPostgresPlugin` and `GetSchemaPlugin`.
     - Create a `ChatCompletionAgent` that uses these plugins.
     - Process a sample user input (e.g., "Show me top 5 rows from the actor table").
     - Display the SQL query results in the output.

## How It Works

1. **QueryPostgresPlugin:**
   - Connects to the PostgreSQL database using `psycopg2`.
   - Cleans and executes the provided SQL query.
   - Retrieves the query results and formats them as a string.

2. **GetSchemaPlugin:**
   - Connects to the PostgreSQL database.
   - Retrieves schema details (table schema, table name, column name, and data type) from the `information_schema.columns` view.
   - Formats the schema details as a human-readable string.

3. **ChatCompletionAgent:**
   - Integrates the above plugins into a semantic kernel-based chat agent.
   - Processes user input to determine whether to retrieve schema information or execute a SQL query.
   - Combines plugin outputs to generate a final SQL query and returns the results to the user.

## Logging and Debugging

- **Logging Configuration:**
  - The project uses the semantic kernel’s logging utilities to provide insight into the agent’s behavior.
  - You can enable detailed logging by adjusting the logging level, for example:
    ```python
    import logging
    logging.getLogger("kernel").setLevel(logging.DEBUG)
    ```
- **Debugging:**
  - Detailed logs will show information about plugin calls, SQL query execution, and agent responses.
  - Use the printed output from each stage (e.g., connection status, query results, error messages) to troubleshoot issues.
  - Ensure environment variables are correctly set to avoid connection errors.

## License

This project is licensed under the [MIT License](LICENSE).



