<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>AskDB — Natural Language to SQL Query System</title>

<style>
:root{
    font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
}

body{
    margin:0;
    padding:40px;
    background:#ffffff;
    color:#111827;
}

main{
    max-width:1000px;
    margin:auto;
}

h1{
    font-size:2.4rem;
    margin-bottom:10px;
}

h2{
    margin-top:40px;
    border-bottom:1px solid #e5e7eb;
    padding-bottom:8px;
}

h3{
    margin-top:20px;
}

p{
    line-height:1.7;
}

ul{
    line-height:1.8;
}

pre{
    background:#f6f8fa;
    padding:16px;
    border-radius:10px;
    overflow:auto;
    border:1px solid #e5e7eb;
}

code{
    background:#f3f4f6;
    padding:3px 6px;
    border-radius:6px;
}

table{
    width:100%;
    border-collapse:collapse;
    margin-top:16px;
}

th,td{
    border:1px solid #e5e7eb;
    padding:12px;
    text-align:left;
}

th{
    background:#f9fafb;
}

blockquote{
    border-left:4px solid #6366f1;
    padding:12px;
    background:#f9fafb;
    margin:20px 0;
}

img{
    width:100%;
    border-radius:14px;
    border:1px solid #e5e7eb;
    margin-top:20px;
}

.note{
    background:#f3f4f6;
    padding:14px;
    border-radius:10px;
    margin-top:12px;
}

.badge{
    display:inline-block;
    background:#eef2ff;
    padding:4px 10px;
    border-radius:20px;
    margin-right:6px;
    font-size:0.85rem;
}
</style>
</head>

<body>
<main>

<h1>🚀 AskDB — Natural Language to SQL Query System</h1>

<p>
AskDB is an <strong>AI-powered backend system</strong> that allows users to query relational databases using
<strong>plain English instead of writing SQL</strong>.
</p>

<p>
It converts natural language questions into SQL queries, executes them on a connected database,
and returns <strong>clear, human-readable answers</strong>.
</p>

<p>
This project demonstrates how <strong>Large Language Models (LLMs)</strong> integrate with traditional
databases using <strong>LangChain orchestration, vector similarity, and structured prompting</strong>
in a production-style architecture.
</p>

---

<h2>🔥 What Problem Does AskDB Solve?</h2>

<p>Accessing data from databases traditionally requires:</p>

<ul>
<li>Knowledge of SQL</li>
<li>Understanding of table schemas</li>
<li>Writing joins, filters, and aggregations manually</li>
</ul>

<p>This creates friction for:</p>

<ul>
<li>Business users</li>
<li>Analysts</li>
<li>Product managers</li>
<li>Non-database engineers</li>
</ul>

<p><strong>AskDB removes this barrier.</strong></p>

<blockquote>
“Show me customers in France with a credit limit over 20,000.”
</blockquote>

<p>AskDB automatically handles:</p>

<ul>
<li>Schema understanding</li>
<li>SQL generation</li>
<li>Query execution</li>
<li>Result explanation</li>
</ul>

---

<h2>✨ Key Features</h2>

<ul>
<li>Natural Language → SQL using LLMs (Google Gemini via LangChain)</li>
<li>Works with any SQL database (MySQL, PostgreSQL, SQLite, SQL Server)</li>
<li>Schema-aware query generation</li>
<li>Conversation-aware follow-ups</li>
<li>REST API built with Flask</li>
<li>Modular production-style pipeline</li>
<li>Database-agnostic execution via SQLAlchemy</li>
</ul>

---

<h2>🏗️ System Architecture</h2>

<p>
The diagram below illustrates the complete <strong>Natural Language → SQL pipeline</strong>,
showing how user queries flow through LLM-driven components before reaching the database.
</p>

<img 
src="https://raw.githubusercontent.com/achyutuni2001/AskDB/3706dc4997922ba3931379b9888f418600b2ca77/diagram-export-1-29-2026-11_49_40-AM.png"
alt="AskDB Architecture Diagram"
/>

<h3>Pipeline Overview</h3>

<pre><code>User → Flask API → Context Manager → Table Selector
      → Example Retriever → SQL Generator → SQL Validator
      → Database → Rephraser → Final Answer
</code></pre>

---

<h2>📁 Project Structure</h2>

<pre><code>AskDB/
├── code1.py
├── untitled0.py
├── database_table_descriptions.csv
├── requirements.txt
├── README.md
├── SETUP.md
├── TECHNICAL.md
├── API.md
└── test.py
</code></pre>

<h3>File Responsibilities</h3>

<table>
<tr><th>File</th><th>Purpose</th></tr>
<tr><td><code>code1.py</code></td><td>Flask API entry point defining <code>/api</code></td></tr>
<tr><td><code>untitled0.py</code></td><td>Core AI engine (LangChain + NL→SQL + execution)</td></tr>
<tr><td><code>database_table_descriptions.csv</code></td><td>Schema descriptions for accurate table selection</td></tr>
<tr><td><code>SETUP.md</code></td><td>Deployment guide</td></tr>
<tr><td><code>TECHNICAL.md</code></td><td>Deep AI architecture</td></tr>
<tr><td><code>API.md</code></td><td>API contract and examples</td></tr>
</table>

---

<h2>🧠 How AskDB Works</h2>

<ol>
<li>User submits a natural language question</li>
<li>Conversation history is loaded</li>
<li>Relevant tables are identified</li>
<li>Similar examples retrieved via embeddings</li>
<li>LLM generates SQL using few-shot prompting</li>
<li>SQL is validated and cleaned</li>
<li>Query executes against the database</li>
<li>Results are converted into natural language</li>
</ol>

---

<h2>🔌 API Usage</h2>

<h3>Endpoint</h3>

<pre><code>POST /api</code></pre>

<h3>Local URL</h3>

<pre><code>http://localhost:5000/api</code></pre>

<div class="note">
The Flask server defines this route using:
<code>@app.route("/api", methods=["POST"])</code>
</div>

<h3>Request</h3>

<pre><code>{
"question": "What is the price of 1968 Ford Mustang?"
}</code></pre>

<h3>Response</h3>

<pre><code>{
"answer": "The price of 1968 Ford Mustang is $95,000."
}</code></pre>

---

<h2>⚙️ Installation</h2>

<h3>Prerequisites</h3>

<ul>
<li>Python 3.8+</li>
<li>SQL database</li>
<li>Google Gemini API key</li>
<li>LangChain API key</li>
</ul>

<h3>Install Dependencies</h3>

<pre><code>pip install -r requirements.txt</code></pre>

<h3>Environment Variables</h3>

<pre><code>export GOOGLE_API_KEY="your_key"
export LANGCHAIN_API_KEY="your_key"
</code></pre>

<h3>Run Server</h3>

<pre><code>python code1.py</code></pre>

---

<h2>🧩 Tech Stack</h2>

<span class="badge">Python</span>
<span class="badge">Flask</span>
<span class="badge">LangChain</span>
<span class="badge">Google Gemini</span>
<span class="badge">SQLAlchemy</span>
<span class="badge">ChromaDB</span>

---

<h2>🔐 Security Best Practices</h2>

<ul>
<li>Never commit API keys</li>
<li>Use environment variables</li>
<li>Prefer read-only DB users</li>
<li>Add authentication before public deployment</li>
<li>Use HTTPS in production</li>
</ul>

---

<h2>⚠️ Current Limitations</h2>

<ul>
<li>Read-only queries</li>
<li>Accuracy tied to schema quality</li>
<li>LLM latency impacts response time</li>
</ul>

---

<h2>🚧 Future Enhancements</h2>

<ul>
<li>Authentication & RBAC</li>
<li>Query caching</li>
<li>UI dashboard</li>
<li>Audit logs</li>
<li>Multi-database federation</li>
</ul>

---

<h2>⭐ Final Note</h2>

<p>
AskDB reflects <strong>real-world AI + backend architecture</strong>, making it ideal for:
</p>

<ul>
<li>Portfolio projects</li>
<li>Technical interviews</li>
<li>Enterprise AI tools</li>
<li>Internal data platforms</li>
</ul>

</main>
</body>
</html>
