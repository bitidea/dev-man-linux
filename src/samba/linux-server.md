# Linux 服务器

## smb.conf

```bash
sudo vim /etc/samba/smb.conf
```

```samba
[global]
    workgroup = WORKGROUP
    dns proxy = no
    log file = /var/log/samba/log.%m
    max log size = 1000
    syslog = 0
    panic action = /usr/share/samba/panic-action %d
    server role = standalone server
    passdb backend = tdbsam
    obey pam restrictions = yes
    unix password sync = yes
    passwd program = /usr/bin/passwd %u
    passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
    pam password change = yes
    map to guest = bad user
    usershare allow guests = no

[home]
    comment = home_dir
    path = /home/jerry
    public = no
    valid users = jerry
    write list = jerry
```

⚠️注意修改以下变量：

* `path`
* `valid users`
* `write list`

## 添加 samba 用户

```bash
smbpasswd -a <USERNAME>
```
