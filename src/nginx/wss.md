# WSS

```nginx
location /websocket {
    proxy_pass http://127.0.0.1:8080/websocket;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
}
```
