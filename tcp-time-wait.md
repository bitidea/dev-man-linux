# 高并发服务器调小 TCP 的 time_wait 超时时间

操作系统默认 240 秒后，才会关闭处于 `time_wait` 状态的连接。

在高并发访问下，服务器端会因为处于 `time_wait` 的连接数太多，可能无法建立新的连接，所以需要在服务器上调小此等待值。

```bash
vim /etc/sysctl.conf
```

```text
net.ipv4.tcp_fin_timeout = 30
```

```bash
sysctl -p
```

OR

```bash
echo "net.ipv4.tcp_fin_timeout = 30" >> /etc/sysctl.conf
sysctl -p
```
