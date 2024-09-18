# Upgrade Node
Upgrade the Master by upgrade `kubelet`

> Check current version of `kubeadm`
```shell
kubeadm version -o short
```

> Check current version of `kubectl` `api & master components`
```shell
kubectl version --short
```

## Cordon the Node

> Cordon the Node using `kubectl` command
```shell
kubectl cordon k8s-node-01
```

## Drain the Node

> Drain the Node using `kubectl` command

```shell
kubectl drain k8s-node-01
```

## Upgrade `kubelet` package

> Upgrade `kubelet` package
```shell
apt-mark unhold kubelet
apt install -y kubelet=1.27.3-00
apt-mark hold kubelet
```

## Upgrade `kubectl` package

> Upgrade `kubectl` package
```shell
apt-mark unhold kubectl
apt install -y kubeadm=1.27.3-00
apt-mark hold kubectl
```

## UnCordon the Node

> UnCordon the Node using `kubectl` command
```shell
kubectl uncordon k8s-node-01
```
> Check current version of `kubeadm`
```shell
kubeadm version -o short
```

> Check current version of `kubectl` `api & master components`
```shell
kubectl version --short
```