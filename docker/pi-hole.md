# Pi-hole

https://hub.docker.com/r/pihole/pihole

https://github.com/pi-hole/pi-hole

## 启动服务器，并将配置文件映射到宿主机

```bash
docker run -d \
  --name pihole \
  -p 53:53/tcp -p 53:53/udp \
  -p 80:80 \
  -p 443:443 \
  -e TZ="Asia/Shanghai" \
  -v "$(pwd)/etc-pihole/:/etc/pihole/" \
  -v "$(pwd)/etc-dnsmasq.d/:/etc/dnsmasq.d/" \
  --dns=127.0.0.1 --dns=1.1.1.1 \
  --restart=unless-stopped \
  pihole/pihole:latest
```

## 启动服务器，不映射配置

```bash
docker run -d \
  --name pihole \
  -p 53:53/tcp -p 53:53/udp \
  -p 80:80 \
  -p 443:443 \
  -e TZ="Asia/Shanghai" \
  --dns=127.0.0.1 --dns=1.1.1.1 \
  --restart=unless-stopped \
  pihole/pihole:latest
```

## 修改密码

```bash
docker exec -it pihole /bin/bash
pihole -a -p password
```
