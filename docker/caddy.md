# Caddy

https://hub.docker.com/_/caddy

## 初始化数据目录

```bash
mkdir caddy_data
```

## 编辑 Caddyfile

```bash
vim Caddyfile
```

## 安装并挂载数据目录

```bash
docker run -d -p 80:80 \
  -v $PWD/Caddyfile:/etc/caddy/Caddyfile \
  -v $PWD/caddy_data:/data \
  caddy
```
