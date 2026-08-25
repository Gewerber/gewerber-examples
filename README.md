# 🧪 Gewerber Examples

Deployment examples, Docker Compose setups, demo projects, and quickstart
configurations for **Gewerber**.

Part of the [Gewerber GitHub organization](https://github.com/Gewerber).

---

## 📦 Contents

Runnable, self-contained examples — each in its own directory with its own
`README.md`:

| Example | What it does |
|---|---|
| [`self-hosted/`](self-hosted/) | Standalone OSS deployment of the backend (Serverpod + PostgreSQL + Redis) on your own server: simplified Compose file, `.env.example`, quickstart with secret generation, backup/restore via the upstream scripts. Single-tenant, no reverse proxy required. |
| [`dev-environment/`](dev-environment/) | Local test PostgreSQL for running the backend's integration tests (`dart test`), modeled after the backend's own `postgres_test` service. |

### Production deployment

The production-grade deployment (Traefik, TLS, resource limits, CI-driven
deploys, backup/restore runbook) lives in the backend repo, not here:
[`gewerber-backend/deploy/`](https://github.com/Gewerber/gewerber-backend/blob/main/deploy/README.md).
The `self-hosted/` example above is derived from it.

## 🗺️ Planned

Not here yet:

- Demo / quickstart projects for individual OSS modules (invoicing, time tracking)
- Deployment examples for [gewerber-app](https://github.com/Gewerber/gewerber-app) and the [website](https://github.com/Gewerber/gewerber-website)
- Sample integrations against the generated API client

Open-core only: no examples for closed modules (banking, tax/ELSTER,
employees, subscriptions, AI assistant).

---

## 🧭 Related

- [Backend](https://github.com/Gewerber/gewerber-backend)
- [App](https://github.com/Gewerber/gewerber-app)
- [Documentation](https://github.com/Gewerber/gewerber-docs)
- [Contributing Guide](https://github.com/Gewerber/.github/blob/main/CONTRIBUTING.md)

---

## 📄 License

Licensed under the [MIT License](LICENSE).
