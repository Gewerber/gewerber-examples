# Dev environment — test database for the Gewerber backend

A single throwaway PostgreSQL 16 (pgvector) container used by the
[Gewerber backend](https://github.com/Gewerber/gewerber-backend)
integration tests. Modeled after the backend's own `postgres_test` service
([`gewerber_backend_server/docker-compose.yaml`](https://github.com/Gewerber/gewerber-backend/blob/main/gewerber_backend_server/docker-compose.yaml))
so you can run `dart test` without cloning any extra infrastructure.

No secrets involved: the default password is a well-known local dummy.

## What it provides

| | |
|---|---|
| Host port | `9090` (override with `POSTGRES_TEST_PORT`) |
| Database | `gewerber_backend_test` |
| User / password | `postgres` / `postgres` (override with `POSTGRES_TEST_PASSWORD`) |

These values match the server's test config,
[`config/test.yaml`](https://github.com/Gewerber/gewerber-backend/blob/main/gewerber_backend_server/config/test.yaml)
(`localhost:9090`, db `gewerber_backend_test`, user `postgres`).

## Run the backend integration tests

Prerequisites: Docker, [Dart SDK](https://dart.dev) (^3.12), a clone of
[gewerber-backend](https://github.com/Gewerber/gewerber-backend).

```bash
# 1. Start the test database (from this directory)
docker compose up -d

# 2. From the backend repo root, fetch workspace dependencies
cd gewerber-backend && dart pub get

# 3. Make sure the test password matches your container.
#    Tests read the DB password from gitignored config/passwords.yaml.
#    With the defaults above you need exactly this under gewerber_backend_server/config/passwords.yaml:
#
#    test:
#      database: postgres
#
#    (plus the other `test:` keys the server expects on startup — copy the
#     section layout from the upstream repo docs/README; never commit the file)

# 4. Run the integration tests (from gewerber-backend/)
cd gewerber_backend_server && dart test
```

Conventions, required setup (`configureDependencies()` in `setUpAll`,
rollback-per-test behaviour) and the full pre-PR checklist are documented in
the backend's [`AGENTS.md`](https://github.com/Gewerber/gewerber-backend/blob/main/AGENTS.md).

## Overrides & troubleshooting

- **Port 9090 busy** → run `docker compose up -d` with
  `POSTGRES_TEST_PORT=9091`, and change `port:` in the server's
  `config/test.yaml` accordingly.
- **Different password** → set `POSTGRES_TEST_PASSWORD=...` before `up`, and
  mirror it in `test.database` of `config/passwords.yaml`.
- **Stale schema/data** after a Serverpod upgrade → reset the volume:
  `docker compose down -v && docker compose up -d`.
- **Tests hang at startup** → check `docker compose ps`; wait for the
  `healthy` status or inspect `docker compose logs postgres_test`.

This stack is for tests only — do not point a running development server at
it; use the backend's `postgres` service (port 8090) for that.
