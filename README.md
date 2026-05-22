# Europa — Student-Built Research Assistant Demo (LangChain-Powered LLM Agent)

[![Live Demo](https://img.shields.io/badge/Live%20Demo-research--agent.onrender.com-46a2f1?logo=render&logoColor=white)](https://research-agent.onrender.com)

Europa is a portfolio project by a **University of Maryland student studying Information Science and Electrical Engineering with a Business minor**. It demonstrates an agent-style research workflow that turns a question into a source-linked draft response.

Built around a **LangChain-based agent architecture** (`langchain-core` + `langchain-community`) with configurable model/provider wiring for LLM-backed synthesis.

## What Europa is (and is not)
- **Is:** a demo research assistant that shows planning, retrieval, synthesis, and report generation.
- **Is not:** a fact-checking service or a guarantee of correctness.
- **Intended use:** portfolio/interview review of system design, API engineering, and transparent AI workflow decisions.

## How It Works
1. **User submits research query**.
2. **Agent decomposes the request into sub-questions** for coverage and planning.
3. **Web search/retrieval tooling gathers candidate sources** (or deterministic sample sources in demo mode).
4. **Validator scores source credibility** and identifies quality signals.
5. **Summarizer synthesizes a draft answer** from retrieved evidence.
6. **Citation report is generated** so claims remain traceable to sources.

## Retrieval mode (explicit)
Europa supports two retrieval modes:

1. **Static sample-data mode (default for demos)**
   - `scripts/demo_pipeline.py` reads from `data/sample/sample_sources.json`.
   - No live web calls.
   - Best for repeatable walkthroughs.

2. **Live lightweight web retrieval (optional)**
   - Backend search service can call **Wikipedia OpenSearch** and **DuckDuckGo Instant Answer**.
   - Useful to demonstrate retrieval plumbing, but coverage/quality varies.

> In short: portfolio demos are usually run in **static sample-data mode**, with **optional live API retrieval** when you want to show networked search behavior.

## Pipeline overview
Europa follows a simple pipeline:

**Search → Retrieve → Synthesize → Output**

Supporting capabilities include source cards, confidence heuristics, contradiction/coverage signals, and trace events for review.

## Example Output
See [`examples/sample_output.md`](examples/sample_output.md) for a full example run.

```text
Query: What are the latest developments in RAG systems as of 2025?
Sub-questions:
  1) Which architecture changes improved retrieval quality?
  2) What evaluation benchmarks are commonly used?
  3) How are teams reducing hallucinations in production?

Summary (excerpt):
Modern RAG systems increasingly combine hybrid retrieval, reranking, and structured grounding
workflows. Production teams are using citation-first generation patterns, guardrail validators,
and offline + online evaluation loops to improve factuality and reliability.
```

## Repo Topics (for GitHub Settings)
To keep repository metadata aligned, set these GitHub topics:
- `langchain`
- `openai` (if using OpenAI models/providers in deployment)
- `web-search`
- `retrieval`

## Limitations (read first)
- Outputs may be incomplete, outdated, or wrong.
- LLM-generated synthesis can hallucinate or misinterpret sources.
- Confidence/validation signals are heuristics, not proof.
- Live retrieval connectors are lightweight and may miss important evidence.
- **Human verification is required before using results for real decisions.**

## Quick start

### 1) Clone and install
```bash
git clone https://github.com/RyanJBush/Autonomous-research-and-intelligence-agent.git
cd Autonomous-research-and-intelligence-agent
make backend-install
make frontend-install
```

### 2) Configure environment and secrets
Create `backend/.env` with at least:
```env
ASTRA_DATABASE_URL=postgresql+psycopg://astra:astra@localhost:5432/astra
ASTRA_JWT_SECRET=change-me-for-local-dev
```

For a Docker-only local demo, `docker-compose.yml` already sets default local environment values.

### 3) Run a local demo

#### Option A (recommended): deterministic CLI demo
```bash
python scripts/demo_pipeline.py
```

#### Option B: local web UI + API
```bash
docker compose up --build
```
- UI: `http://localhost:5173`
- API docs: `http://localhost:8000/docs`

## Example research session (deterministic demo)
1. Run `python scripts/demo_pipeline.py`.
2. Enter a research question when prompted.
3. Review produced source list and synthesized report draft.
4. Manually verify important claims against trusted sources.

## Portfolio Preview and screenshots
- Portfolio Preview page: `docs/preview/index.html`
- Screenshot guide: `docs/screenshots/README.md`
- Architecture: `docs/architecture.md`
- Demo runbook: `docs/demo-runbook.md`

## Resume bullets
See `docs/resume-bullets.md`.

## License
MIT (see `LICENSE`).
