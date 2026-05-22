# AI Research & Competitive Intelligence Agent

## Executive Summary
This project is a recruiter-ready **AI Research & Competitive Intelligence Agent** that automates a multi-stage research workflow from user query to structured report output. It demonstrates practical LLM-style orchestration patterns in Python, including planning, source discovery, extraction, validation heuristics, summarization, and report generation. The system includes a FastAPI backend, a React frontend, and a deterministic CLI demo for portfolio demonstration and technical interviews.

## Business/Research Problem This Project Solves
AI, data, and business teams often spend too much time manually breaking down broad questions, gathering scattered sources, and assembling findings into usable outputs. This project standardizes that process by turning one query into a traceable workflow with source filtering, contradiction detection, confidence scoring, and structured reporting. It helps teams produce faster first-pass research drafts that are easier to review and refine.

## Key Features
- **Research plan generation:** Decomposes a query into sub-questions with objectives and expected source types.
- **Automated source discovery:** Searches via DuckDuckGo Instant Answer API and Wikipedia OpenSearch.
- **Web content extraction:** Pulls page title and paragraph content from discovered URLs.
- **Validation and filtering:** Applies domain allow/deny lists, deduplication, prompt-injection signal checks, and minimum content thresholds.
- **Credibility scoring:** Assigns source type, credibility score, and confidence label using heuristic scoring.
- **Contradiction detection:** Flags potentially conflicting claims and assigns severity levels.
- **PII-aware processing:** Redacts emails, phone numbers, and SSN patterns before storage/reporting.
- **Structured outputs:** Produces executive summary, findings, evidence table, open questions, contradictions, and conclusion in a report schema.
- **Citation excerpts:** Builds citation markers and excerpts linked to source records.
- **Traceability and observability:** Stores stage-level trace events, per-agent run metrics, and aggregate research metrics.
- **Iteration controls:** Supports configurable depth/breadth/max sources and optional refinement passes when confidence is low.
- **Multiple interfaces:** Includes REST API endpoints, React UI, and a local demo pipeline script.

## Tech Stack
- **Backend:** Python 3.11+, FastAPI, SQLAlchemy, Pydantic
- **Frontend:** React, Vite, Tailwind CSS
- **Data layer:** PostgreSQL (via psycopg), Docker Compose for local orchestration
- **Research tooling:** requests, BeautifulSoup4
- **LLM workflow ecosystem:** langchain-core, langchain-community, FAISS-backed memory store
- **Quality tooling:** pytest, ruff, ESLint, Prettier

## Agent Workflow Overview
1. **Planning** – Build a structured plan from the query.
2. **Searching** – Generate query variants and collect candidate URLs.
3. **Extracting** – Fetch and normalize source content.
4. **Validating** – Filter sources, score credibility, and detect contradictions.
5. **Synthesizing** – Build structured report outputs and summary text.

The backend records trace events and agent metrics across these stages for replay and analysis.

## Input-to-Output Process
**Input**
- Research query
- Optional controls: depth, breadth, recency window, max sources, allow/deny domains, confidence threshold

**Processing**
- Query decomposition into plan steps
- Search query expansion and URL discovery
- HTML extraction and text normalization
- Source validation, credibility scoring, contradiction checks, and PII redaction
- Citation extraction and report assembly

**Output**
- Structured report object (JSON) with executive summary, findings, evidence table, contradictions, open questions, and conclusion
- Human-readable summary text
- Exportable report formats via API (JSON, Markdown, PDF)
- Trace timeline and metrics endpoints for run diagnostics

## Setup and Installation
### 1) Clone and install dependencies
```bash
git clone https://github.com/RyanJBush/ai-research-and-competitive-intelligence-agent.git
cd ai-research-and-competitive-intelligence-agent
make backend-install
make frontend-install
```

### 2) Configure backend environment
Create `backend/.env`:
```env
ASTRA_DATABASE_URL=postgresql+psycopg://astra:astra@localhost:5432/astra
ASTRA_JWT_SECRET=change-me-for-local-dev
ASTRA_DAILY_RESEARCH_QUOTA=20
```

### 3) Run locally
**CLI demo (sample data pipeline):**
```bash
python scripts/demo_pipeline.py
```

**Full app (Postgres + API + UI):**
```bash
docker compose up --build
```
- Frontend: `http://localhost:5173`
- API docs: `http://localhost:8000/docs`

## Example Use Cases
- Competitive intelligence briefs for AI products and vendors
- AI engineering research on tools, model practices, and governance trends
- Business analytics background research to support strategy memos
- Data analysis scoping by collecting and comparing external evidence sources
- Workflow automation demonstrations for analyst/research productivity

## Skills Demonstrated
- Multi-stage AI workflow orchestration and stateful pipeline design
- Prompt/query decomposition and iterative retrieval strategy
- Information extraction, normalization, and heuristic validation
- Structured report generation with confidence and evidence signals
- Prompt-injection-aware filtering and basic PII redaction integration
- Python backend engineering with typed schemas and service-layer architecture
- API design, frontend integration, and reproducible local development setup

## Resume-Ready Project Description
Built an **AI Research & Competitive Intelligence Agent** using Python, FastAPI, SQLAlchemy, and React to automate research planning, source discovery, extraction, validation, and structured report generation. Implemented credibility scoring, contradiction detection, citation excerpting, PII redaction hooks, and traceable stage metrics to improve consistency and speed for AI engineering, data analysis, business analytics, and workflow automation research tasks.

## Future Improvements
- Add more retrieval connectors beyond current Wikipedia/DDG-based discovery.
- Improve extraction quality for complex page layouts and non-HTML sources.
- Add benchmark datasets and automated evaluation for report quality.
- Expand analyst controls for human review workflows and approvals.
- Strengthen ranking/reranking and source deduplication strategies.
