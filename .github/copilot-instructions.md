# Copilot Instructions

## Nature of the repo
No application source code here. It is a Docker Compose harness for the OpenClassrooms "Jardin Actuel" blog app (test-training project). Backend (Symfony 6.2) and frontend (Angular 15.2) ship as prebuilt images from `ghcr.io/openclassrooms-student-center/` (`jardin-actuel-backend:2-0-0`, `jardin-actuel-frontend:2-0-0`). There is no build, lint, or test tooling in the repo; tests are written externally against the running stack.

## Commands
- Start: `docker compose up -d`
- Stop: `docker compose down`
- Health check (backend): `curl -f http://localhost:8081/api/health`
- Reset DB: `docker compose down -v` then `docker compose up -d`. The init SQL only runs when the `mysql-data` volume is empty.

## Architecture
- `jardin-actuel-bdd` (MariaDB 11.7.2): DB `jardin_actuel`, user/password `jardin`/`jardin`. Mounts `./data` as `/docker-entrypoint-initdb.d` (seed SQL, run on first init only) and the named volume `mysql-data` as the data dir. Do not bind-mount the data dir from `/mnt/c` (WSL): world-writable perms make MariaDB ignore `.my-healthcheck.cnf`, so the healthcheck fails.
- `jardin-actuel-symfony` (API, port 8081): configured via `DATABASE_URL` env var pointing at `jardin-actuel-bdd:3306`. Starts only after the DB healthcheck passes.
- `jardin-actuel-angular` (UI, port 8080 → 80): starts after the API healthcheck passes.
- All services share the `symfony` network. Startup order is enforced with `depends_on` + `service_healthy`.
- Schema (Doctrine): `category`, `comment`, `post`, `user`, `doctrine_migration_versions`.

## Conventions / gotchas
- Seed SQL exists in two places: `data/diay0794_jardinactuel.sql` and `data/data/diay0794_jardinactuel.sql`. Only the top-level one in `data/` is picked up by the container's init; keep them in sync if editing.
- README is in French; keep user-facing docs in French.
