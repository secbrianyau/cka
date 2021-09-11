# Using Namespaces

Get namespaces:

```
kubectl get namespaces
```

Get resources in a specified namespace:

```
kubectl get pods --namespace my-namespace
kubectl get pods -n my-namespce
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
kubectl drain <node> --ignore daemonsets
```

If the node remains part of the cluster, you can allow pods to run on the node again when maintenance is complete:

```
kubectl uncordon <node>
```

