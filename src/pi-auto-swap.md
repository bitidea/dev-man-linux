# 树莓派自动调整 Swap 分区

```bash
sudo vim /etc/dphys-swapfile
```

把 `CONF_SWAPSIZE=100` 注释掉

```bash
sudo systemctl restart dphys-swapfile
```
