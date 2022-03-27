# BBR

[https://github.com/google/bbr](https://github.com/google/bbr)

内核版本 >= 4.9

```bash
echo "net.core.default_qdisc = fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control = bbr" >> /etc/sysctl.conf
sysctl -p
lsmod | grep bbr
```
