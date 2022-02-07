# 负载均衡

```nginx
http {
    upstream backend {
        # ip_hash;
        server backend1.example.com;
        server backend2.example.com;
    }

    server {
        listen 80;
        listen [::]:80;

        server_name _;

        location / {
            proxy_pass http://backend;
        }
    }
}
```
