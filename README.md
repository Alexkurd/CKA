# CKA

## Create resources

### Create pod
kubectl run nginx --image=nginx

### Create pod template
kubectl run nginx --image=nginx --labels=env=prod --dry-run=client -o yaml > nginx_pod.yaml

### Create deployment
kubectl create deploy --image=nginx nginx

### Create deployment template
kubectl create deploy --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

### Create daemonset
To create a daemonset, use Create deployment template file and change the kind and remove replicas & strategy.

### Create service
kubectl expose pod valid-pod --port=444 --name=frontend

### Create configmap app-config with env=dev:
kubectl create configmap app-config --from-literal=env=dev

### Create secret app-secret with pass=123:
kubectl create secret generic app-secret --from-literal=pass=123


## Cluster maintenance

### Cluster upgrade(kubeadm)

1. Controlplane
apt update
apt upgrade kubeadm=1.26.0-00
kubeadm upgrade plan
kubeadm upgrade apply v1.26.0

2. Worker Nodes
apt update
apt upgrade kubeadm=1.26.0-00
kubeadm upgrade node

3. Kubelet/Kubectl(all nodes)
apt-get install -y kubelet=1.26.0-00 kubectl=1.26.0-00
systemctl daemon-reload
systemctl restart kubelet
