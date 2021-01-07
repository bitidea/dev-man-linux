# 镜像加速器

https://yeasy.gitbook.io/docker_practice/install/mirror

```bash
sudo vim /etc/docker/daemon.json
```

```json
{
    "registry-mirrors": [
        "https://ustc-edu-cn.mirror.aliyuncs.com",
        "https://kk24uads.mirror.aliyuncs.com"
    ]
}
```
