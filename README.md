```md
# AskDB – Natural Language to SQL Query System

AskDB is an AI-powered backend system that allows users to query relational databases using **plain English** instead of writing SQL.  
It converts natural language questions into SQL queries, executes them on a connected database, and returns **clear, human-readable answers**.

This project demonstrates how **Large Language Models (LLMs)** can be integrated with traditional databases using **LangChain**, **vector similarity**, and **structured prompting** in a production-style architecture.

---

## 🚀 What Problem Does AskDB Solve?

Accessing data from databases traditionally requires:

- Knowledge of SQL
- Understanding of table schemas
- Writing joins, filters, and aggregations manually

This creates friction for:

- Business users
- Analysts
- Product managers
- Non-database engineers

**AskDB removes this barrier** by allowing users to ask questions like:

> “Show me customers in France with a credit limit over 20,000”

and automatically handling:

- Schema understanding
- SQL generation
- Query execution
- Result explanation

---

## ✨ Key Features

- **Natural Language → SQL** using LLMs (Google Gemini via LangChain)
- **Works with any SQL database**  
  (MySQL, PostgreSQL, SQLite, SQL Server)
- **Schema-aware query generation** using table descriptions
- **Conversation-aware follow-ups** (multi-turn context supported)
- **REST API** built with Flask
- **Modular, production-style pipeline**
- **Database-agnostic execution** using SQLAlchemy

---

## 🏗️ High-Level Architecture

```

User (English Question)
↓
Flask REST API (code1.py)
↓
Conversation Context Manager
↓
Table Selection (LLM + Structured Output)
↓
Example Retrieval (Vector Similarity)
↓
SQL Generation (Few-Shot Prompting)
↓
SQL Cleaning & Validation
↓
Database Execution (SQLAlchemy)
↓
Answer Rephrasing (LLM)
↓
Final Natural Language Response

```

---

## 📁 Project Structure

```

AskDB/
├── code1.py
├── untitled0.py
├── database_table_descriptions.csv
├── requirements.txt
├── README.md
├── SETUP.md
├── TECHNICAL.md
├── API.md
└── test.py

````

### File Responsibilities

| File | Purpose |
|---|---|
| `code1.py` | Flask API entry point (defines `/api`) |
| `untitled0.py` | Core AI engine (LangChain + NL→SQL + execution + rephrasing) |
| `database_table_descriptions.csv` | Human-readable schema descriptions used for table selection |
| `requirements.txt` | Python dependencies |
| `README.md` | High-level project overview (this file) |
| `SETUP.md` | Detailed setup & deployment guide |
| `TECHNICAL.md` | Deep technical architecture (chains, embeddings, vector store, etc.) |
| `API.md` | Full API contract + examples + error handling |
| `test.py` | Local testing & experiments |

---

## 🧠 How AskDB Works (Step-by-Step)

1. User submits a question in natural language  
2. Conversation history is loaded (for follow-ups)  
3. Relevant database tables are identified (schema-aware selection)  
4. Similar example queries are retrieved using embeddings (vector similarity)  
5. SQL is generated using few-shot prompting  
6. Generated SQL is cleaned and validated (removes formatting artifacts)  
7. SQL is executed against the database  
8. Raw results are converted into a natural language answer  

---

## 🧪 Example Queries

- List all customers in France with credit limit over 20,000
- What is the highest payment ever made?
- Show top 5 products by sales
- How many orders were placed last month?
- What is the total revenue this year?

### Context-Aware Follow-ups

AskDB maintains conversation context, so follow-up questions work naturally:

- What about the ones from Germany?
- Show their recent orders

---

## 🔌 API Usage

AskDB exposes a single REST endpoint for asking questions.

### Endpoint

```http
POST /api
````

### Full Local URL

```http
http://localhost:5000/api
```

> **Where does `/api` come from?**
> The Flask server in `code1.py` defines a route like:
> `@app.route("/api", methods=["POST"])`
> That route is the public entry point into the AskDB pipeline.

### Request Body

```json
{
  "question": "What is the price of 1968 Ford Mustang?"
}
```

### Response

```json
{
  "answer": "The price of 1968 Ford Mustang is $95,000."
}
```

### Example cURL Request

```bash
curl -X POST http://localhost:5000/api \
  -H "Content-Type: application/json" \
  -d '{
    "question": "List all customers in France with credit limit over 20000"
  }'
```

### Error Responses (Typical)

**400 Bad Request**

```json
{ "error": "Missing 'question' in the request body" }
```

**500 Internal Server Error**

```json
{ "error": "Database connection failed" }
```

---

## ⚙️ Installation & Setup (Quick)

### Prerequisites

* Python 3.8+
* Any SQL database
* Google AI (Gemini) API key
* LangChain API key

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Environment Variables

```bash
export GOOGLE_API_KEY="your_google_api_key"
export LANGCHAIN_TRACING_V2="true"
export LANGCHAIN_PROJECT="askdb"
export LANGCHAIN_API_KEY="your_langchain_api_key"
```

### Database Configuration

Update the DB connection inside `untitled0.py`:

```python
# MySQL
db = SQLDatabase.from_uri("mysql+pymysql://user:password@host:port/database")

# PostgreSQL
db = SQLDatabase.from_uri("postgresql://user:password@host:port/database")

# SQLite
db = SQLDatabase.from_uri("sqlite:///path/to/database.db")
```

### Table Descriptions (Required)

Create or update `database_table_descriptions.csv`:

```csv
table_name,description
customers,"Customer information including country and credit limit"
orders,"Order data with dates and total amounts"
products,"Product catalog with pricing and category details"
```

> This file is critical for accurate table selection and prevents hallucinated queries.

### Run the Server

```bash
python code1.py
```

Server runs at:

```text
http://localhost:5000
```

---

## 🧩 Tech Stack

* **Backend**: Python, Flask
* **LLM Orchestration**: LangChain
* **Model**: Google Gemini (via `langchain-google-genai`)
* **Database Access**: SQLAlchemy (+ driver e.g., PyMySQL)
* **Vector Store**: ChromaDB
* **Embeddings**: Google Generative AI embeddings

---

## 🔐 Security Considerations

* Store API keys in environment variables (never commit secrets)
* Use a **read-only database user** in production
* Add authentication (API key/JWT) before exposing publicly
* Use HTTPS in production environments

---

## ⚠️ Current Limitations

* Read-only query support
* Accuracy depends on schema description quality
* Latency depends on LLM response time and query complexity

---

## 🚧 Future Enhancements

* Authentication & role-based access control
* Query result caching
* UI dashboard
* Query explainability + audit logs
* Multi-database federation

---

## 🧾 Documentation Index

* **README.md** — Project overview (this file)
* **SETUP.md** — Detailed setup & deployment
* **TECHNICAL.md** — Internal architecture & AI pipeline
* **API.md** — Full API reference & usage examples

---

## ✅ Final Note

AskDB is structured to reflect **real-world backend + AI system design**, making it suitable for:

* Portfolio projects
* Technical interviews
* AI-powered internal tools
* Data exploration services

