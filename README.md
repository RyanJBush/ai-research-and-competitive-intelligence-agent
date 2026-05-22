# AI Research & Competitive Intelligence Agent

This project is a recruiter-ready portfolio implementation of an **AI Research & Competitive Intelligence Agent** that turns a broad question into a structured, evidence-linked research report. It demonstrates practical LLM workflow design with planning, source discovery, extraction, validation heuristics, summarization, and report generation. The system is built to support transparent decision-making and faster analyst workflows while keeping a human reviewer in the loop.

## Business / Research Problem This Project Solves
Analysts and AI teams often spend significant time manually breaking down ambiguous questions, collecting scattered sources, and assembling findings into decision-ready outputs. This project automates that research pipeline by decomposing queries, collecting candidate sources, extracting content, and producing structured report artifacts with confidence and coverage signals. The result is a repeatable workflow for competitive intelligence and technical research drafts that improves speed, consistency, and traceability.

## Key Features
- **Automated research planning:** Generates structured sub-questions, objectives, and expected source types from a user query.
- **Iterative retrieval workflow:** Expands search queries and can generate follow-up queries based on unsupported claims.
- **Live lightweight source discovery:** Uses DuckDuckGo Instant Answer API and Wikipedia OpenSearch for candidate URL retrieval.
- **Content extraction stage:** Pulls page title/content payloads for downstream analysis.
- **Credibility and quality heuristics:** Applies source validation, credibility scoring, contradiction checks, and evidence coverage signals.
- **LLM-style synthesis outputs:** Produces executive summaries, findings, open questions, and conclusions in structured report format.
- **Citation-linked reporting:** Builds claim support objects and source evidence tables for auditability.
- **PII-aware processing hooks:** Includes redaction support integrated into the orchestration layer.
- **Traceable orchestration:** Persists stage events, metrics, and run artifacts for replay and review.
- **Multiple interfaces:** Deterministic CLI demo pipeline plus FastAPI backend and React frontend for interactive usage.

## Tech Stack
- **Language:** Python (backend and pipeline scripts), JavaScript (frontend).
- **Backend framework:** FastAPI + SQLAlchemy.
- **Frontend:** React + Vite.
- **LLM workflow ecosystem:** LangChain core/community dependencies in project stack.
- **Data/runtime:** PostgreSQL-compatible database configuration and Docker Compose local runtime.
- **Testing:** Pytest-based backend test suite.

## Agent Workflow Overview
The orchestration pipeline in `ResearchService` follows these stages:
1. **Planning** — create a structured research plan from the query.
2. **Searching** — generate search variants and collect candidate URLs.
3. **Extracting** — fetch and normalize source content payloads.
4. **Validating** — score source quality and detect contradictions.
5. **Synthesizing** — generate summary/report outputs with evidence links.

This design mirrors real-world AI agent patterns: decomposition, tool use, evaluation, and structured generation.

## Input-to-Output Process
**Input:**
- User research query
- Optional controls such as depth, breadth, recency window, source caps, and allow/deny domain lists

**Processing:**
- Query decomposition and sub-question generation
- Search query expansion and source collection
- Source extraction and filtering
- Credibility, contradiction, and evidence-coverage analysis
- Citation/report assembly

**Output:**
- Structured research report (JSON/markdown-ready)
- Executive summary and findings with confidence levels
- Evidence table, contradictions, open questions, and conclusion
- Run traces/metrics for observability

## Setup and Installation
### 1) Clone and install dependencies
```bash
git clone https://github.com/RyanJBush/Autonomous-research-and-intelligence-agent.git
cd Autonomous-research-and-intelligence-agent
make backend-install
make frontend-install
```

### 2) Configure backend environment
Create `backend/.env`:
```env
ASTRA_DATABASE_URL=postgresql+psycopg://astra:astra@localhost:5432/astra
ASTRA_JWT_SECRET=change-me-for-local-dev
```

### 3) Run locally
**Deterministic CLI demo (sample data):**
```bash
python scripts/demo_pipeline.py
```

**Full local app (API + UI):**
```bash
docker compose up --build
```
- Frontend: `http://localhost:5173`
- API docs: `http://localhost:8000/docs`

## Example Use Cases
- Competitive landscape research brief generation
- AI engineering trend scans (tools, architectures, benchmarks)
- Data/business analytics exploratory research summaries
- First-pass evidence gathering for product or strategy memos
- Workflow automation demos for analyst productivity portfolios

## Skills Demonstrated
- Multi-stage AI workflow orchestration
- Prompt and query decomposition strategies
- Information extraction and normalization pipelines
- Summarization and structured report generation
- Evidence/credibility heuristic design
- API-first backend engineering with typed schemas
- Human-in-the-loop reliability framing and AI safety mindset
- Reproducible demos and test-driven backend development

## Resume-Ready Project Description
Built an **AI Research & Competitive Intelligence Agent** that automates question decomposition, source discovery, extraction, validation, and structured report generation. Engineered a Python/FastAPI + React system with traceable pipeline stages, credibility/coverage heuristics, contradiction checks, and citation-linked outputs to accelerate research workflows for AI engineering, data analysis, business analytics, and automation use cases.

## Future Improvements
- Add broader, configurable retrieval connectors beyond current lightweight APIs.
- Integrate stronger ranking/reranking and deduplication strategies.
- Expand extraction robustness for diverse content formats.
- Add evaluation datasets and regression benchmarks for report quality.
- Improve interactive analyst controls for review, approval, and feedback loops.
- Introduce role-based workflow templates for domain-specific research tasks.

## Important Limitations
- This system provides draft research outputs and heuristic confidence signals, not guaranteed truth.
- Live retrieval is lightweight and may miss important or higher-quality evidence.
- Human verification is required before using outputs for real decisions.
