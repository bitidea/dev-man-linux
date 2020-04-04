# Redis

https://hub.docker.com/_/redis

## 启动 Redis 实例（没有持久化存储）

```bash
docker run -p 6379:6379 --name redis -d redis
```

## 启动 Redis 实例（持久化存储）

并将数据目录挂载到宿主机的 `/docker-data/redis/data` 目录下

```bash
docker run -p 6379:6379 \
    --name some-redis \
    -v /docker-data/redis/data:/data \
    -d redis redis-server --appendonly yes
```

持久化存储说明：https://redis.io/topics/persistence
