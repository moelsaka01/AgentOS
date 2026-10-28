# AOS, Agent Orchestration System

AOS is a recruiter-facing agent systems project with four major pillars:

- Multi-agent orchestration
- Provider routing for Groq or OpenAI
- Persistent vector memory with ChromaDB
- A built-in evaluation and benchmark lab

This project demonstrates practical AI systems engineering concepts beyond a simple LLM wrapper, including agent coordination, memory persistence, evaluation workflows, and observability.

AOS is a portfolio-grade implementation and does not claim parity with production systems developed by OpenAI, Anthropic, or other frontier AI laboratories.

## What is inside

- **Modern dashboard** for runs, metrics, traces, memory, and evaluations
- **Provider routing**
  - Groq as a no-cost starting option
  - OpenAI as an optional paid provider
  - Demo fallback when no API key is configured
- **Multi-agent runtime**
  - Planner
  - Researcher
  - Executor
  - Critic
  - Reflector
  - Memory service
- **Vector memory** with ChromaDB persistence
- **Evaluation system**
  - Seeded benchmark datasets
  - Benchmark suites executable from the dashboard
  - Stored evaluation runs and per-case results
  - Pass-rate and aggregate-score trends
  - Failure review panel
- **CLI benchmark runner** for repeatable testing

## System architecture

AOS separates provider interaction, agent orchestration, persistent memory, evaluation, and dashboard functionality into distinct modules.

The primary architectural components are:

| Component | Responsibility |
|---|---|
| Agent runtime | Coordinates agent execution and refinement workflows |
| Provider layer | Handles Groq, OpenAI, and demo fallback |
| Vector memory | Stores and retrieves semantic memory using ChromaDB |
| Evaluation engine | Executes benchmark suites and records results |
| Benchmark runner | Provides command-line access to evaluation suites |
| Dashboard | Exposes runs, metrics, traces, memory, and evaluations |

## Benchmark suites included

- `core_reasoning`
- `memory_benchmark`
- `math_and_tools`

## Prerequisites

Before running AOS, ensure that you have:

- Git installed
- Docker Desktop with Docker Compose, or a compatible Python environment
- A Groq or OpenAI API key if you want to use a real LLM provider

Docker is the recommended starting option because it simplifies environment setup.

## Recommended no-cost setup

Use Groq.

1. Copy `.env.example` to `.env`.
2. Add your Groq API key to `GROQ_API_KEY`.
3. Leave `LLM_PROVIDER=auto`.
4. Start the application using Docker.

**Security:** Never commit `.env` files, API keys, credentials, or other secrets to GitHub.

## Run with Docker

```bash
docker compose up --build
```

Once the application is running, open:

```text
http://localhost:8000
```

To stop the application, press `Ctrl+C` in the terminal.

## Run without Docker

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

Or on Linux/macOS:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the application:

```bash
uvicorn app.main:app --reload
```

Open:

```text
http://localhost:8000
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

The evaluation system supports repeatable benchmark execution, stored results, and failure analysis.

## Runtime configuration

AOS exposes several environment variables for controlling runtime depth and refinement behavior.

| Environment variable | Example value | Purpose |
|---|---|---|
| `AOS_RUNTIME_DEPTH` | `deep` | Selects the configured runtime depth |
| `AOS_MIN_REFINEMENT_ROUNDS` | `2` | Controls the minimum refinement rounds |
| `AOS_PLAN_EXPANSION_ROUNDS` | `2` | Controls planning expansion rounds |
| `AOS_RESEARCH_PASSES` | `2` | Controls research passes |
| `AOS_MAX_REFLECTION_ROUNDS` | `3` | Controls the maximum reflection rounds |

Example configuration:

```dotenv
AOS_RUNTIME_DEPTH=deep
AOS_MIN_REFINEMENT_ROUNDS=2
AOS_PLAN_EXPANSION_ROUNDS=2
AOS_RESEARCH_PASSES=2
AOS_MAX_REFLECTION_ROUNDS=3
```

Increasing runtime depth may increase latency and provider usage. Appropriate settings depend on the workload and available resources.

## Troubleshooting

### Application does not start

If the Docker-based application fails to start:

1. Confirm Docker Desktop is running.
2. Check that Docker Compose is available.
3. Review the terminal output for errors.
4. Rebuild the application:

```bash
docker compose up --build
```

### Dashboard is not accessible

If `http://localhost:8000` does not open:

1. Verify the application started successfully.
2. Confirm port `8000` is not already occupied.
3. Review the container logs:

```bash
docker compose logs
```

### LLM provider is not responding

If provider requests fail:

1. Confirm the correct API key is configured.
2. Check that the selected provider is available.
3. Verify network connectivity.
4. Inspect application logs for provider errors.
5. Confirm that the provider account has the necessary quota or credits.

### Benchmark execution fails

If a benchmark suite fails:

1. Confirm the application dependencies are installed.
2. List available benchmark suites:

```bash
python -m app.benchmark_runner --list
```

3. Verify that the selected suite exists.
4. Inspect the error output to identify configuration, provider, or dataset issues.

## Main files

```text
app/
  main.py                # Routes, dashboard APIs, schema bootstrap, eval APIs
  agent_runtime.py       # Multi-agent orchestration
  llm.py                 # Groq/OpenAI/demo provider layer
  vector_memory.py       # ChromaDB-backed semantic memory store
  tools.py               # Calculator and memory tools
  models.py              # Runs, traces, memories, evaluation tables
  evals.py               # Benchmark seeding, judging, suite execution
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

**Enterprise AI architecture**

Design a production-ready multi-agent AI system for enterprise document analysis. Include memory, tool usage, evaluation loops, failure handling, architecture, data flow, and tradeoffs.

**Memory demonstration**

Remember that our system prioritizes reliability over speed and targets enterprise clients in regulated industries.

**Cost estimation**

Estimate the monthly cost of running an AI system with 50,000 daily users, 8 API calls per user at $0.001 per call, and propose optimizations.

**Planning and refinement**

Propose a rollout plan for an AI SaaS product, then critique your plan, identify weaknesses, and improve it.

## Evaluation scope and limitations

AOS provides a portfolio-oriented evaluation environment with repeatable datasets, stored scorecards, benchmark trends, and failure review.

However, its evaluation system should not be considered equivalent to frontier-laboratory evaluation infrastructure.

The project focuses on demonstrating AI engineering concepts, including:

- Repeatable evaluation workflows
- Agent orchestration
- Provider abstraction
- Persistent semantic memory
- Runtime observability
- Benchmark-driven iteration

## Contributing

Contributions that improve reliability, documentation, evaluation coverage, and developer experience are welcome.

Suggested contribution areas include:

- Improving installation and troubleshooting documentation
- Expanding benchmark datasets
- Adding evaluation test cases
- Improving runtime error handling
- Strengthening provider integration tests
- Enhancing observability and tracing

For substantial changes, open an issue to discuss the proposed improvement before implementation.

When submitting a pull request:

1. Create a descriptive feature or fix branch.
2. Make a focused change.
3. Run relevant checks or tests.
4. Explain the purpose of the change in the PR description.
5. Submit the pull request for review.

## Project status

AOS is a portfolio-grade AI systems engineering project intended to demonstrate practical architecture, experimentation, and evaluation workflows.

It is not presented as a production-certified platform.

## License

Refer to the repository's `LICENSE` file, if present, for applicable licensing terms.
