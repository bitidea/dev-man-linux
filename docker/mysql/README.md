# MySQL

https://hub.docker.com/_/mysql

## 服务器

### 运行所有服务（MySQL + Adminer）

```bash
docker-compose up -d
```

### 单独运行 MySQL

```bash
docker-compose up -d db
```

## 命令行客户端

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
