# MariaDB

https://hub.docker.com/_/mariadb


```bash
docker run \
  --name mariadb \
  -e MYSQL_ROOT_PASSWORD=toor \
  -p 3306:3306 \
  -d mariadb:latest \
  --character-set-server=utf8mb4 \
  --collation-server=utf8mb4_unicode_ci
```
