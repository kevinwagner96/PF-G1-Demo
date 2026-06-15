# PF-G1-Demo Agent Notes

## Purpose
Docker Compose launcher for the full PF-G1 demo. This repo does not contain application code; it builds the app services from sibling project folders or the scheduler repository declared in `docker-compose.yml`.

## Services
- `db`: PostgreSQL 16.
- `back`: builds `PF-G1-Back-Django`.
- `scheduler`: builds `pf-or-scheduler` from `scheduler-api`.
- `front`: builds `PF-G1-Front`.

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
- Django Back applies migrations on startup.
- Front must call Django Back, never Scheduler directly.
