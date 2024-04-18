# Linux 服务器

```bash
sudo apt install samba samba-common-bin -y
```

```bash
sudo mkdir -m 1777 /opt/smbshare
```

## 配置文件

```bash
sudo vim /etc/samba/smb.conf
```

添加到文件末尾：

```conf
[smbshare]
path = /opt/smbshare
writeable=Yes
create mask=0777
directory mask=0777
public=no
```

## 创建 SMB 用户

```bash
sudo smbpasswd -a smb
```

`\\192.168.1.23\smbshare`
