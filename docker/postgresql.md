# PostgreSQL

https://hub.docker.com/_/postgres

```bash
docker run -d \
  --name postgres \
  -e POSTGRES_PASSWORD=postgres \
  -p 5432:5432 \
  postgres
```
