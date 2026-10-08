# 🤖 TaskBot — AI-Powered Task Management Agent

> Manage your todos using natural language with an AI agent powered by LangChain, Groq, and SQLite.

TaskBot is an AI-powered task management assistant that allows users to manage their tasks through simple natural-language conversations.

Instead of manually writing SQL queries, users can simply ask TaskBot to create, view, update, or delete tasks. The AI agent understands the request and interacts with the SQLite database using LangChain's SQL tools.

---

## ✨ Features

- 🤖 Natural-language task management
- ➕ Create new tasks using conversational commands
- 📋 View and search existing tasks
- ✏️ Update task details and status
- ✅ Mark tasks as completed
- 🗑️ Delete tasks
- 🔎 SQL-powered database querying
- 🧠 AI agent powered by LangChain
- ⚡ Groq-powered LLM inference
- 💾 SQLite database for persistent task storage
- 🧵 Conversation memory using LangGraph
- 🛡️ SQL operation and task validation
- 📊 Structured task output

---

## 🧠 How It Works

TaskBot converts natural-language requests into database operations through an AI agent.

```text
                User
                  │
                  ▼
          Natural Language
                  │
                  ▼
        ┌──────────────────┐
        │     TaskBot      │
        │    AI Agent      │
        └────────┬─────────┘
                 │
                 ▼
          LangChain Agent
                 │
                 ▼
        SQL Database Tools
                 │
                 ▼
          SQLite Database
                 │
                 ▼
              tasks
              table
```

### Example

```text
User:
"Create a task to make a video for Rapid Global News"

        ↓

AI Agent understands the request

        ↓

SQL INSERT operation

        ↓

Task stored in SQLite

        ↓

TaskBot:
"Task created successfully."
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| LangChain | AI agent and SQL tool integration |
| Groq | LLM inference |
| LangGraph | Agent execution and memory |
| SQLite | Task database |
| SQLAlchemy | Database connectivity |
| python-dotenv | Environment variable management |
| uv | Python package and environment management |

---

## 📂 Project Structure

```text
SQL-AGENT/
│
├── sql_agent.py
├── my_tasks.db
├── .env
├── .gitignore
├── pyproject.toml
├── uv.lock
└── README.md
```

> `my_tasks.db` is generated locally when the application runs and should not be committed to GitHub.

---

## 🗄️ Database Schema

TaskBot uses a SQLite database with a `tasks` table.

```sql
CREATE TABLE IF NOT EXISTS tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    description TEXT,
    status TEXT CHECK(
        status IN ('pending', 'in_progress', 'completed')
    ) DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Task Fields

| Field | Description |
|---|---|
| `id` | Unique task ID |
| `title` | Task title |
| `description` | Detailed task description |
| `status` | Current task status |
| `created_at` | Task creation timestamp |

### Available Statuses

```text
pending
in_progress
completed
```

---

## 💬 Example Commands

TaskBot understands natural-language requests.

### Create a Task

```text
Create a task called Learn LangChain
```

```text
Create a task "I have to make video"
with description "Video for Rapid Global News for YouTube, Instagram, Facebook and X"
```

### View Tasks

```text
Show me all my tasks
```

```text
Show my pending tasks
```

```text
Show my latest 5 tasks
```

```text
Which tasks are completed?
```

### Update a Task

```text
Mark task 3 as completed
```

```text
Move task 2 to in progress
```

### Delete a Task

```text
Delete task 5
```

---

## 🔄 CRUD Operations

TaskBot supports complete CRUD functionality.

```text
CREATE
  ↓
INSERT INTO tasks

READ
  ↓
SELECT FROM tasks

UPDATE
  ↓
UPDATE tasks

DELETE
  ↓
DELETE FROM tasks
```

After modifying a task, the agent verifies the operation using a SQL query before confirming the result to the user.

---

## 🔐 Environment Variables

Create a `.env` file in the root directory:

```env
GROQ_API_KEY=your_groq_api_key
```

Never commit your `.env` file to GitHub.

---

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/taskbot-sql-ai-agent.git
cd taskbot-sql-ai-agent
```

### 2. Install Dependencies

If you are using `uv`:

```bash
uv sync
```

### 3. Configure Environment Variables

Create a `.env` file:

```bash
touch .env
```

Add your Groq API key:

```env
GROQ_API_KEY=your_groq_api_key
```

### 4. Run the Application

```bash
uv run python sql_agent.py
```

---

## 🖥️ Usage

After starting the application, you will see:

```text
user :
```

Enter a natural-language request.

For example:

```text
user : Create a task to learn LangGraph
```

TaskBot processes the request and interacts with the SQLite database.

You can continue chatting:

```text
user : Show all my tasks

user : Mark task 1 as completed

user : Show my completed tasks
```

To exit:

```text
exit
```

or:

```text
quit
```

---

## 🧠 AI Agent Capabilities

The agent is designed to:

- Understand natural-language task requests
- Select the appropriate SQL tool
- Generate SQL queries
- Execute database operations
- Verify CREATE, UPDATE, and DELETE operations
- Handle task statuses
- Detect ambiguous task requests
- Return structured task information

---

## 🛡️ Safety Rules

TaskBot follows several database safety rules:

- SELECT queries are limited to a maximum of 10 results by default.
- Task lists are ordered by creation time.
- Task IDs are never invented.
- Ambiguous tasks require clarification.
- Destructive database operations such as `DROP TABLE` are not allowed.
- Database modifications are verified after execution.
- API keys and environment variables are not exposed.

---

## 🎯 Example Workflow

```text
User:
Create a task to prepare my AI interview

        ↓

TaskBot:
Creates task in SQLite

        ↓

User:
Show my pending tasks

        ↓

TaskBot:
Queries SQLite

        ↓

┌────┬──────────────────────────┬─────────┐
│ ID │ Title                    │ Status  │
├────┼──────────────────────────┼─────────┤
│ 1  │ Prepare AI interview     │ pending │
└────┴──────────────────────────┴─────────┘

        ↓

User:
Mark task 1 as completed

        ↓

TaskBot:
Updates database and verifies the change

        ↓

Task #1 has been marked as completed.
```

---

## 📌 Future Improvements

- [ ] Web-based chat interface
- [ ] User authentication
- [ ] Multiple-user task management
- [ ] Task priorities
- [ ] Due dates and reminders
- [ ] Task categories
- [ ] Search and filtering
- [ ] PostgreSQL support
- [ ] REST API using FastAPI
- [ ] Cloud deployment
- [ ] Streaming AI responses
- [ ] Rich task-management dashboard

---

## 📚 What I Learned

Building this project helped me understand:

- AI agent architecture
- LangChain SQL agents
- LLM tool calling
- Natural-language-to-SQL workflows
- SQLite database operations
- CRUD operations
- LangGraph memory and checkpointing
- Prompt engineering
- Environment variable management
- AI + database integration

---

