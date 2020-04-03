# Nextcloud

https://hub.docker.com/_/nextcloud

```bash
docker run -d \
  --name=nextcloud \
  -p 8888:80 \
  -v /docker-data/nextcloud:/var/www/html \
  nextcloud
```
