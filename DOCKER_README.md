# Docker development

This `docker-compose.yml` runs three services:

- `db` - PostgreSQL (image `postgres:15`). Host port `5433` is mapped to the container's `5432` to keep compatibility with local config.
- `backend` - Spring Boot application (built with Gradle inside the image). Exposes `8080`.
- `frontend` - React app built with Vite and served by `nginx`. Exposes host port `5173`.

Quick start (from `demo-backend` folder):

```powershell
docker compose build
docker compose up
```

Notes:

- The Spring Boot app reads DB connection from `SPRING_DATASOURCE_URL` (overridden by docker-compose to `jdbc:postgresql://db:5432/demo_db`).
- Postgres credentials are set to `postgres` / `1234` in the compose file. Adjust if needed and keep secrets out of source control in production.
- To run only backend and db: `docker compose up db backend`.
