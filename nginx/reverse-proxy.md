# 反向代理

## 普通反向代理

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8000;
    }
}
```

## 跨域反向代理

跨域说明：http://www.ruanyifeng.com/blog/2016/04/cors.html

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name _;

    location / {
        add_header Access-Control-Allow-Origin *;
        add_header Access-Control-Allow-Methods *;
        add_header Access-Control-Allow-Headers *;

        if ($request_method = 'OPTIONS') {
            return 204;
        }

        proxy_pass http://127.0.0.1:8000;
    }
}
```
