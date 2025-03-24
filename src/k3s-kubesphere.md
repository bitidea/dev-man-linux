# K3S + KubeSphere

## K3S

[https://docs.rancher.cn/docs/k3s/quick-start/\_index](https://docs.rancher.cn/docs/k3s/quick-start/_index)

### Master

#### 安装最新稳定版本

```bash
curl -sfL http://rancher-mirror.cnrancher.com/k3s/k3s-install.sh | INSTALL_K3S_MIRROR=cn sh -
```

#### kubeconfig 文件

```bash
cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
```

#### node-token

```bash
cat /var/lib/rancher/k3s/server/node-token
```

### Worker

#### 安装最新稳定版本

```bash
curl -sfL http://rancher-mirror.cnrancher.com/k3s/k3s-install.sh | INSTALL_K3S_MIRROR=cn K3S_URL=https://myserver:6443 K3S_TOKEN=mynodetoken sh -
```

### 配置 containerd 镜像

```bash
vim /etc/rancher/k3s/registries.yaml
```

```yaml
mirrors:
  "docker.io":
    endpoint:
      - "https://ustc-edu-cn.mirror.aliyuncs.com"
```

```bash
systemctl restart k3s.service
```

### 卸载 K3S

#### Master 卸载

```bash
/usr/local/bin/k3s-uninstall.sh
```

#### Worker 卸载

```bash
/usr/local/bin/k3s-agent-uninstall.sh
```

## KubeSphere

[https://kubesphere.io/docs/quick-start/minimal-kubesphere-on-k8s/](https://kubesphere.io/docs/quick-start/minimal-kubesphere-on-k8s/)

### 安装

#### 国际互联网顺畅

```bash
k3s kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.2.1/kubesphere-installer.yaml

k3s kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.2.1/cluster-configuration.yaml
```

#### 国际互联网受限

```bash
k3s kubectl apply -f https://download.fastgit.org/kubesphere/ks-installer/releases/download/v3.2.1/kubesphere-installer.yaml

k3s kubectl apply -f https://download.fastgit.org/kubesphere/ks-installer/releases/download/v3.2.1/cluster-configuration.yaml
```

### 信息

```text
IP:30880
```

```text
admin
P@88w0rd
```

### 进入面板

```bash
ssh -L 30880:127.0.0.1:30880 -N -T -v root@SERVER_IP
```

[http://127.0.0.1:30880](http://127.0.0.1:30880)

### 从 Kubernetes 上卸载 KubeSphere

[https://kubesphere.io/zh/docs/installing-on-kubernetes/uninstall-kubesphere-from-k8s/](https://kubesphere.io/zh/docs/installing-on-kubernetes/uninstall-kubesphere-from-k8s/)

```bash
wget https://raw.githubusercontent.com/kubesphere/ks-installer/release-3.1/scripts/kubesphere-delete.sh
```

## K3S Traefik Dashboard

```bash
kubectl get pod -n kube-system
```

```bash
kubectl port-forward traefik-XXX -n kube-system 9000:9000
```

```bash
ssh -L 9000:127.0.0.1:9000 -N -T -v root@SERVER_IP
```

[http://localhost:9000/dashboard/](http://localhost:9000/dashboard/)

## Kuboard

[https://github.com/eip-work/kuboard-press/blob/master/install/v3/install-built-in.md](https://github.com/eip-work/kuboard-press/blob/master/install/v3/install-built-in.md)

请不要使用 `127.0.0.1` 或者 `localhost` 作为内网 IP

```bash
sudo docker run -d \
  --restart=unless-stopped \
  --name=kuboard \
  -p 80:80/tcp \
  -p 10081:10081/tcp \
  -e KUBOARD_ENDPOINT="http://内网IP:80" \
  -e KUBOARD_AGENT_SERVER_TCP_PORT="10081" \
  -v /root/kuboard-data:/data \
  eipwork/kuboard:v3
```
