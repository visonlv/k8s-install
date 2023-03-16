#  安装nfs分布式文件系统

## 1 安装服务
```
sudo apt install -y nfs-kernel-server
sudo mkdir -p /data/k8s/
sudo chown nobody:nogroup /data/k8s/
sudo vim /etc/exports 
    /data/k8s/ *(rw,sync,no_subtree_check)
    /data/storageclass/ *(rw,sync,no_subtree_check)
sudo exportfs -ra
sudo systemctl enable nfs-server
sudo systemctl restart nfs-kernel-server
systemctl status nfs-kernel-server
showmount -e 10.55.134.242

其中遇到pod一直启动失败
需要修改配置添加 - --feature-gates=RemoveSelfLink=false

find / -name  kube-apiserver.yaml
vim /etc/kubernetes/manifests/kube-apiserver.yaml
kubectl apply -f /etc/kubernetes/manifests/kube-apiserver.yaml

  containers:
  - command:
    - kube-apiserver
    - --feature-gates=RemoveSelfLink=false
    - --advertise-address=10.55.134.241
    - --allow-privileged=true
    - --authorization-mode=Node,RBAC
```

## 2 安装客户端
```
sudo apt-get install nfs-common
mkdir -p /data/k8s/
sudo mount -t nfs -o nolock -o tcp 10.55.134.242:/data/k8s/ /data/k8s/
sudo umount /data/k8s
##sudo umount -lf /data/k8s
```

## 3 k8s使用nfs
```
```