# 高可用集群

## check-nginx-pid.sh

```bash
sudo vim /usr/local/src/check-nginx-pid.sh
```

```bash
#!/bin/bash
CHECK_CMD=`ps -C nginx --no-header | wc -l`
RESTART_CMD=`/usr/sbin/nginx`
if [ $CHECK_CMD -eq 0 ];then
    # restart nginx
    $RESTART_CMD
    # if restart nginx failed
    if [ $CHECK_CMD -eq 0 ];then
        exit 1
    else
        exit 0
    fi
else
    exit 0
fi
```

## Master - keepalived.conf

```bash
sudo vim /etc/keepalived/keepalived.conf
```

```nginx
global_defs {
    router_id nginx_master
}
vrrp_script chk_http_port {
    script "/usr/local/src/check-nginx-pid.sh"
    interval 2
    weight 2
}
vrrp_instance VI_1 {
    state MASTER
    interface ens33
    virtual_router_id 66
    priority 100
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass p_sS
    }
    track_script {
        chk_http_port
    }
    virtual_ipaddress {
        172.16.91.199
    }
}
```

## Backup - keepalived.conf

```bash
sudo vim /etc/keepalived/keepalived.conf
```

```nginx
global_defs {
    router_id nginx_backup
}
vrrp_script chk_http_port {
    script "/usr/local/src/check-nginx-pid.sh"
    interval 2
    weight 2
}
vrrp_instance VI_1 {
    state BACKUP
    interface ens33
    virtual_router_id 66
    priority 99
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass p_sS
    }
    track_script {
        chk_http_port
    }
    virtual_ipaddress {
        172.16.91.199
    }
}
```
