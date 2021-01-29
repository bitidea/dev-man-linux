# iptables 恢复默认设置

```bash
# 默认策略设置为 ACCEPT，否则后续操作会导致连接断开，无法再次连接
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
sudo iptables -t nat -P PREROUTING ACCEPT
sudo iptables -t nat -P POSTROUTING ACCEPT
sudo iptables -t nat -P OUTPUT ACCEPT
# 清空所有规则
sudo iptables -F
sudo iptables -t nat -F
# 删除所有非系统默认的链
sudo iptables -X
sudo iptables -t nat -X
```
