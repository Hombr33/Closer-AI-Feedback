# 📞 Closer AI Sales Call Evaluator

## Overview

**Closer AI Sales Call Evaluator** is a robust, production-grade platform for analyzing sales call transcripts using OpenAI GPT-4, LangChain, and Supabase. It provides detailed, actionable feedback for sales teams, detects business rule violations at the chunk level, and supports advanced analytics, automation, and reporting.

---

## ✨ Key Features

- **Automated Transcript Analysis**: Processes and chunks transcripts, embedding each chunk for context-aware evaluation.
- **Dynamic Business Rules**: Enforce and update business rules (e.g., currency, compliance) at the chunk level, with violation detection and scoring penalties.
- **Reference-Based Scoring**: Compares each chunk to high-quality reference calls using vector search (Pinecone).
- **Chunk-Level & Aggregated Reporting**: Returns detailed JSON for each chunk and a comprehensive, aggregated final report.
- **Async Analysis & Webhook Notification**: Supports background processing and notifies external systems (e.g., Make.com) on completion.
- **Supabase Integration**: Stores all calls, analyses, business rules, and analytics in a scalable cloud database.
- **Leaderboard & Analytics**: Team and individual performance dashboards, coaching insights, and time-based metrics.
- **Admin Controls**: Secure authentication, call and rule management, and audit logging.
- **Prompt Logging**: All LLM prompts are logged for transparency and debugging.
- **API-First**: FastAPI backend with endpoints for all major operations.

---

## 🗂️ Project Structure

```
closer-ai-feedback-langchain/
├── api.py                  # FastAPI backend
├── main.py                 # CLI entry point for local analysis
├── database/
│   └── database_manager.py # Supabase integration and business logic
├── embeddings/
│   ├── embed_good_calls.py # Embedding reference calls
│   └── pinecone_store.py   # Pinecone vector store manager
├── langchain_script/
│   ├── analysis.py         # Core chunk/final analysis logic
│   ├── evaluator.py        # Transcript evaluation pipeline
│   └── transcript_parser.py# Transcript chunking utilities
├── data/
│   └── good_calls/         # Reference transcripts (not in repo)
├── requirements.txt
├── README.md
└── supabase_setup.sql      # Database schema
```

---

## ⚙️ Tech Stack

- **OpenAI GPT-4** – LLM for deep analysis
- **LangChain** – RAG, prompt management, chunking
- **Pinecone** – Vector search for reference matching
- **Supabase** – Cloud PostgreSQL (with RLS, cascade, analytics)
- **FastAPI** – Secure, modern API
- **Make.com** – Workflow automation (webhook integration)
- **Optional**: React + Tailwind CSS frontend

---

## 🚀 Quickstart

### 1. Clone the Repository

```bash
git clone https://github.com/ren-418/closer-ai-feedback-langchain.git
cd closer-ai-feedback-langchain
```

### 2. Install Dependencies

```bash
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

### 3. Configure Environment

Copy `env_template.txt` to `.env` and fill in your values:

```
# Required API Keys
OPENAI_API_KEY=your_openai_key
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your_supabase_key
PINECONE_API_KEY=your_pinecone_key
PINECONE_CLOUD=aws
PINECONE_REGION=us-east-1

# Make.com Webhook (for automation)
MAKE_WEBHOOK_URL=https://hook.us2.make.com/your_webhook_endpoint
```

### 4. Prepare Reference Data

- Place high-quality reference transcripts in `data/good_calls/`
- Run:
  ```bash
  python embeddings/embed_good_calls.py
  ```

### 5. Set Up Supabase

- Run `supabase_setup.sql` in your Supabase SQL editor to create tables and policies.
- If you already have a database, ensure DELETE policies are present for RLS (see `add_delete_policies.sql` if needed).

### 6. Run the API Server

```bash
uvicorn api:app --reload
python api.py
```

### 7. Analyze a Call (CLI)

```bash
python main.py path/to/transcript.txt
```

---

## 🛡️ Security & Data Privacy

- **RLS**: Row Level Security is enabled on all tables.
- **No real transcripts** are included in the repo.
- All prompts and analyses are logged for auditability.

---

## 🧠 Advanced Capabilities

- **Business Rules Engine**: Add, update, or remove rules via API. Violations are detected per chunk and aggregated in reports.
- **Chunk-Level Analysis**: Each transcript is split and analyzed in context, with reference matching and business rule enforcement.
- **Async Processing**: New calls can be submitted for background analysis, with webhook notification on completion.
- **Comprehensive Analytics**: Leaderboards, coaching insights, and time-based performance metrics for teams and individuals.
- **Admin & API Controls**: Secure endpoints for user, closer, call, and rule management.

---

## 📈 Example Use Cases

- **Sales Team Coaching**: Identify strengths, weaknesses, and compliance issues in real calls.
- **QA & Compliance**: Enforce business rules (e.g., currency, legal language) and detect violations in real time.
- **Automated Reporting**: Integrate with Make.com or other tools for workflow automation and notifications.

---

## 🛠️ Roadmap

- [x] Dynamic business rules (API-managed)
- [x] Chunk-level violation detection
- [x] Async analysis & webhook notification
- [x] Analytics dashboard (API)
- [ ] React frontend (optional)
- [ ] More granular RLS policies

---

## 📄 License

Private project — Not open-sourced. Usage permitted only by client or authorized team members.
