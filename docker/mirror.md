# 镜像

https://yeasy.gitbooks.io/docker_practice/install/mirror.html

```bash
sudo vim /etc/docker/daemon.json
```

```json
{
  "registry-mirrors": [
    "https://dockerhub.azk8s.cn",
    "https://reg-mirror.qiniu.com"
  ]
}
```
