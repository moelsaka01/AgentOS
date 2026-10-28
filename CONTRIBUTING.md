# Contributing to AOS

Thank you for your interest in contributing to Agent Orchestration System (AOS).

AOS is an AI systems engineering project focused on multi-agent orchestration, LLM provider routing, persistent memory, and evaluation workflows.

## Ways to Contribute

Contributions are welcome in the following areas:

- Bug fixes and reliability improvements
- Documentation and setup guides
- Evaluation datasets and benchmark coverage
- Multi-agent orchestration improvements
- Provider integration and error handling
- Observability and runtime tracing
- Automated testing

## Development Setup

1. Clone the repository.
2. Copy `.env.example` to `.env`.
3. Configure your provider credentials if needed.
4. Start the application:

```bash
docker compose up --build
```

5. Open `http://localhost:8000`.

## Contribution Workflow

1. Open an issue for substantial proposed changes.
2. Create a branch from the default branch.
3. Make focused, documented changes.
4. Run relevant tests or benchmark suites.
5. Submit a pull request with a clear description.

## Pull Request Guidelines

Each pull request should include:

- A concise description of the change
- The reason for the change
- Relevant testing or validation results
- Screenshots when modifying the dashboard
- References to related issues, if applicable

Avoid including unrelated changes in the same pull request.

## Security

Never commit API keys, `.env` files, passwords, tokens, or other credentials.

If you discover a security vulnerability, avoid publishing exploitation details in a public issue. Contact the repository maintainer privately.

## Code Quality

Prefer readable, maintainable implementations with clear responsibilities.

When modifying agent behavior, memory, or evaluations, document any assumptions and explain relevant tradeoffs.

## Community Expectations

Be respectful, constructive, and professional when discussing issues, reviewing contributions, or proposing improvements.

Thank you for helping improve AOS!
