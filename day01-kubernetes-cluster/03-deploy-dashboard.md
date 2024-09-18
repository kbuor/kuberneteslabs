# Deploy Kubernetes Dashboard
Deploy the dashboard for kubernetes
> Ref. Link: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

## Deploying the dashboard UI

> Download the dashboard.yaml manifest
```shell
wget https://raw.githubusercontent.com/kbuor/Kubernetes/main/manifest/dashboard.yaml
```

> Create the workload and services
```shell
kubectl apply -f dashboard.yaml
```

## Create `kubernetes-dashboard-certs`
> Using OpenSSL to generate SSL self-Certificate
```shell
mkdir certs
chmod -R 777 certs
openssl req -nodes -newkey rsa:2048 -keyout certs/dashboard.key -out certs/dashboard.csr -subj "/C=/ST=/L=/O=/OU=/CN=kubernetes-dashboard"
openssl x509 -req -sha256 -days 365 -in certs/dashboard.csr -signkey certs/dashboard.key -out certs/dashboard.crt
```

> Create secret for `kubernetes-dashboard-certs`
```shell
kubectl create secret generic kubernetes-dashboard-certs --from-file=certs -n kubernetes-dashboard
```

## Create User and Get Token to Login
> Create Service Account
```shell
wget https://raw.githubusercontent.com/kbuor/Kubernetes/main/manifest/service-account.yaml
kubectl apply -f service-account.yaml
```
> Create ClusterRoleBinding
```shell
wget https://raw.githubusercontent.com/kbuor/Kubernetes/main/manifest/cluster-role-binding.yaml
kubectl apply -f cluster-role-binding.yaml
```
> Get token
```shell
kubectl -n kubernetes-dashboard create token admin-user
```

> (Optional) Install K9s
```shell
curl -sS https://webinstall.dev/k9s | bash
```
-----------

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
-----------
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