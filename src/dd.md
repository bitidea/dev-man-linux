# 使用 cat 替代 dd

```bash
# dd version
dd if=image.iso of=/dev/sdb bs=4M
```

```bash
# cat version
cat image.iso >/dev/sdb
```

```bash
# cat version with progress meter
cat image.iso | pv >/dev/sdb
```
