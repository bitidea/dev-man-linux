# Swap

[https://wiki.archlinux.org/index.php/swap](https://wiki.archlinux.org/index.php/swap)

```bash
fallocate -l 2G /swapfile && chmod 600 /swapfile && mkswap /swapfile && swapon /swapfile && echo '/swapfile none swap defaults 0 0' >> /etc/fstab
```
