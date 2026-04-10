# AOS, Agent Orchestration System

AOS is a recruiter-facing agent systems project with four major pillars:

- multi-agent orchestration
- provider routing for Groq or OpenAI
- persistent vector memory with ChromaDB
- a built-in eval and benchmark lab

This is meant to look and feel closer to an AI systems engineering project than a simple LLM wrapper. It is still a portfolio-grade implementation, not a claim of parity with OpenAI or Anthropic production systems.

## What is inside

- **Modern dashboard** for runs, metrics, traces, memory, and evals
- **Real provider routing**
  - Groq as the no-cost starting path
  - OpenAI as an optional paid path
  - demo fallback when no API key is configured
- **Multi-agent runtime**
  - planner
  - researcher
  - executor
  - critic
  - reflector
  - memory service
- **Vector memory** with ChromaDB persistence
- **Eval system**
  - seeded benchmark datasets
  - benchmark suites you can run from the UI
  - stored eval runs and per-case results
  - pass rate and aggregate score trends
  - failure review panel
- **CLI benchmark runner** for repeatable testing

## Benchmark suites included

- `core_reasoning`
- `memory_benchmark`
- `math_and_tools`

## Recommended no-cost setup

Use Groq.

1. Copy `.env.example` to `.env`
2. Put your Groq key into `GROQ_API_KEY`
3. Leave `LLM_PROVIDER=auto`
4. Start the app with Docker

## Run with Docker

```bash
docker compose up --build
```

Then open:

```text
http://localhost:8000
```

## Run without Docker

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

## Run benchmark suites from the command line

List available suites:

```bash
python -m app.benchmark_runner --list
```

Run one suite:

```bash
python -m app.benchmark_runner --suite core_reasoning
```

## Main files

```text
app/
  main.py                # routes, dashboard APIs, schema bootstrap, eval APIs
  agent_runtime.py       # multi-agent orchestration
  llm.py                 # Groq/OpenAI/demo provider layer
  vector_memory.py       # ChromaDB-backed semantic memory store
  tools.py               # calculator + memory tools
  models.py              # runs, traces, memories, eval tables
  evals.py               # benchmark seeding, judging, suite execution
  benchmark_runner.py    # CLI benchmark runner
  templates/dashboard.html
  static/styles.css
  static/app.js

evals/datasets/
  core_reasoning.json
  memory_benchmark.json
  math_and_tools.json
```

## Good demo prompts

- Design a production-ready multi-agent AI system for enterprise document analysis. Include memory, tool usage, evaluation loops, failure handling, architecture, data flow, and tradeoffs.
- Remember that our system prioritizes reliability over speed and targets enterprise clients in regulated industries.
- Estimate the monthly cost of running an AI system with 50,000 daily users, 8 API calls per user at $0.001 per call, and propose optimizations.
- Propose a rollout plan for an AI SaaS product, then critique your plan, identify weaknesses, and improve it.

## Important note

The benchmark system is strong for a portfolio project, but it is not equivalent to frontier-lab internal eval infrastructure. It is a serious step toward that style of engineering: repeatable datasets, stored scorecards, benchmark trends, and failure review.


Runtime depth environment variables:
- AOS_RUNTIME_DEPTH=deep
- AOS_MIN_REFINEMENT_ROUNDS=2
- AOS_PLAN_EXPANSION_ROUNDS=2
- AOS_RESEARCH_PASSES=2
- AOS_MAX_REFLECTION_ROUNDS=3
