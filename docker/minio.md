# MinIO

https://hub.docker.com/r/minio/minio

https://docs.min.io/docs/minio-docker-quickstart-guide

```docker
mkdir -p /docker-data/minio/data
```

```bash
docker run -p 9000:9000 --name minio \
  -e "MINIO_ACCESS_KEY=9383B3C781754BC8B344D4BFB2D74434" \
  -e "MINIO_SECRET_KEY=CF9A7A9ADC594B61AEE79C215B4E7D9D" \
  -v /docker-data/minio/data:/data \
  minio/minio server /data
```
