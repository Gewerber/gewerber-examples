# AGENTS.md — gewerber-examples

Deployment examples, Docker Compose setups, and demo projects for Gewerber.

## Conventions

- Each example lives in its own directory with a dedicated `README.md` explaining what it does and how to run it.
- Keep examples minimal, self-contained, and reproducible.
- Reference the real repositories (`gewerber-backend-core`, `gewerber-app`) rather than duplicating their code.
- Never commit secrets, credentials, or production configuration. Use placeholders and `.env.example` files.

## Open-Core Boundary

Examples must only cover the open-source core. Do not add examples for closed modules (banking, tax/ELSTER, employees, subscriptions, AI assistant).
