# PF-G1-Demo Agent Notes

## Purpose
Docker Compose launcher for the full PF-G1 demo. This repo does not contain application code; it builds the app services from their GitHub repositories.

## Services
- `db`: PostgreSQL 16.
- `back`: builds `PF-G1-Back` from `main`.
- `scheduler`: builds `pf-or-scheduler` from `scheduler-api`.
- `front`: builds `PF-G1-Front` from `main`.

## Commands
```bash
docker compose up --build
docker compose down
docker compose down -v
```

## Rules
- Keep this repo as orchestration only.
- Do not copy app source code here.
- If a service needs a Dockerfile change, make it in that service repo and push it to the branch referenced by `docker-compose.yml`.
- Back applies migrations on startup.
- Front must call Back, never Scheduler directly.
