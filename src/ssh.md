# SSH

## 生成 key

```bash
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
```

## 群发 key

```bash
cat target-host-list | xargs -n 1 ssh-copy-id
```
