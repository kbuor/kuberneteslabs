# Upgrade Master

> Check current version of `kubeadm`
```shell
kubeadm version -o short
```

> Check current version of `kubectl` `api & master components`
```shell
kubectl version --short
```


## Upgrade `kubeadm` package

> Upgrade `kubeadm` package
```shell
apt-mark unhold kubeadm
apt install -y kubeadm=1.27.3-00
apt-mark hold kubeadm
```

## Check upgrade plan

> Check upgrade plan using `kubeadm`: docker, kubeadm, kubelet

```shell
kubeadm upgrade plan
```

## Upgrade Master and Components

> Run the recommand command receive from upgrade plan

```shell
kubeadm upgrade apply <plan>
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

> Check current version of `kubeadm`
```shell
kubeadm version -o short
```

> Check current version of `kubectl` `api & master components`
```shell
kubectl version --short
```