# MySQL

https://hub.docker.com/_/mysql

## Server

### 最新版本

```bash
docker run --name mysql \
    -e MYSQL_ROOT_PASSWORD=toor \
    -p 3306:3306 \
    -d mysql:latest \
    --character-set-server=utf8mb4 \
    --collation-server=utf8mb4_unicode_ci
```

#### 挂载配置、日志、数据目录

```bash
docker run --name mysql \
    -e MYSQL_ROOT_PASSWORD=toor \
    -p 3306:3306 \
    -v /docker-data/mysql/conf:/etc/mysql \
    -v /docker-data/mysql/log:/var/log/mysql \
    -v /docker-data/mysql/data:/var/lib/mysql \
    -d mysql:latest \
    --character-set-server=utf8mb4 \
    --collation-server=utf8mb4_unicode_ci
```

### 5.7 版本

```bash
docker run --name mysql57 \
    -e MYSQL_ROOT_PASSWORD=toor \
    -p 3306:3306 \
    -d mysql:5.7 \
    --character-set-server=utf8mb4 \
    --collation-server=utf8mb4_unicode_ci
```

#### 挂载配置和数据目录

```bash
docker run --name mysql57 \
    -e MYSQL_ROOT_PASSWORD=toor \
    -p 3306:3306 \
    -v /docker-data/mysql/conf:/etc/mysql \
    -v /docker-data/mysql/log:/var/log/mysql \
    -v /docker-data/mysql/data:/var/lib/mysql \
    -d mysql:5.7 \
    --character-set-server=utf8mb4 \
    --collation-server=utf8mb4_unicode_ci
```

## Client

```bash
docker run -it --rm mysql -uroot -h172.17.0.1 -p
```

## MySQL 8.0 错误解决 - Client does not support authentication protocol requested by server

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'toor';
FLUSH PRIVILEGES;
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'toor';
FLUSH PRIVILEGES;
```
