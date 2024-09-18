# Deploy Kubernetes Dashboard
Deploy the dashboard for kubernetes
> Ref. Link: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

## Deploying the dashboard UI

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