# Docker 清理

**⚠️ 危险操作，请谨慎使用**

## 清理所有停止运行的容器

```bash
docker container prune
```

## 清理所有悬挂 none 镜像

```bash
docker image prune
```

## 清理所有无用数据卷

```bash
docker volume prune
```
