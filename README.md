# Using Namespaces

Get namespaces:

```
kubectl get namespaces
```

Get resources in a specified namespace:

```
kubectl get pods --namespace my-namespace
kubectl get pods -n my-namespce -o wide
```

Get resources in all namespaces:

```
kubectl get pods --all-namespaces
```

Create namespace:

```
kubectl create namespace my-namespace
```

---

# K8S Management Overview

## High-Availablilty

- Need multiple control plane nodes
  - Likely need to communicate with the K8S API through a load balancer
  
- Etcd
  - Stacked etcd
  - External etcd
 
 <br/>
 
 ## K8S Management Tools
 
 1. kubectl
 2. kubeadm - Quickly create cluster
 3. minikube - Auto set up a local single node k8s cluster
 4. helm - Template and package management for k8s object s
 5. kompose - help translate docker compose to k8s objects
 6. kustomize - conf management tool for managing k8s objects
 
 <br/>
 
 ## Safely drain k8s nodes
 
 - Drain = Maintenance - Remove a k8s node from service
   - COntainers running on the node will be gracefully terminated; may be rescheduled on another node
 
```
kubectl drain <node>
kubectl drain <node> --ignore-daemonsets
kubectl drain <node> --ignore-daemonsets --force
```

If the node remains part of the cluster, you can allow pods to run on the node again when maintenance is complete:

```
kubectl uncordon <node>
```

<br/>

## Upgrading K8S with kubeadm


Control plane upgrade steps:

1. Upgrade `kubeadm` on the control plane node
2. Drain the control plane node
3. Plan the upgrade `kubeadm upgrade plan`
4. Apply the upgrade `kubeadm upgrade apply`
5. Upgrade `kubelet` and `kubectl` on the control plane node
6. `uncordon` the control plane node


Worker node upgrade steps:

1. Drain the node
2. Upgrade `kubeadm`
3. Upgrade the `kubelet` configuration `kubeadm ugprade node`
4. Upgrade `kubelet` and `kubectl`
5. `uncordon` the node

