# 使用 Nexus 搭建 Docker Registry

## 安装

```bash
docker run -d --name nexus_docker \
  --restart=always \
  -p 8081:8081 \
  -p 8082:8082 \
  --mount src=nexus-docker-data,target=/nexus-data \
  sonatype/nexus3
```

数据目录：`/var/lib/docker/volumes`

## 使用 SSL 隧道进行初始化

```bash
ssh -L 8081:127.0.0.1:8081 -N -T YOUR_SERVER_DOMAIN
```

## 创建 Docker Repository

```
Setting[小齿轮] ->
Repositories ->
Create repository ->
docker(hosted) ->
HTTP 填 8082
```

## 开启 Docker Token Realms

```
Setting[小齿轮] ->
Security ->
Realms ->
激活 Docker Bearer Token Realm
```

## Nginx HTTPS

```nginx
server {
    server_name YOUR_SERVER_DOMAIN;
    listen       443 ssl;

    ssl_certificate /etc/ssl/YOUR_SERVER_DOMAIN.crt;
    ssl_certificate_key /etc/ssl/YOUR_SERVER_DOMAIN.key;

    ssl_session_timeout  5m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers   on;
    large_client_header_buffers 4 32k;
    client_max_body_size 300m;
    client_body_buffer_size 512k;
    proxy_connect_timeout 600;
    proxy_read_timeout   600;
    proxy_send_timeout   600;
    proxy_buffer_size    128k;
    proxy_buffers       4 64k;
    proxy_busy_buffers_size 128k;
    proxy_temp_file_write_size 512k;

    location / {
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Port $server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_redirect off;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_pass http://127.0.0.1:8082;
        proxy_read_timeout 900s;
    }
    error_page   500 502 503 504  /50x.html;
}
```

## Docker Login

```bash
docker login YOUR_SERVER_DOMAIN -u admin -p YOUR_PASSWORD
```
