<p><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/67/Kubernetes_logo.svg/2560px-Kubernetes_logo.svg.png" alt="k8s-logo" title="k8s" align="top" height=100 /></p>

Repository containing all configurations used to deploy my personal Kubernetes lab cluster.

## Cluster design

### Overview

*To be reworked*

### Components

  - **Base OS** : Flatcar Linux 3033.2.3
  - **Kubernetes distribution** : k0s `v1.23.3+k0s.1`
  - **CRI** : containerd
  - **CNI** : Cilium (kube-proxy free mode)
  - **CSI** : OpenEBS
  - **Ingress Controller** : HAProxy Ingress Controller
  - **External Load Balancer** : HAProxy

### Nodes description

  - 1x **HAProxy external LB** for Control Plane entrypoint, nodes registration and workloads (1vCPU/1GB RAM)
  - 3x **Controller** nodes in HA mode with `etcd` cluster embedded (with 2vCPU/2GB RAM each)
  - 3x **Worker** nodes (with 8vCPU/16GB RAM each)

## Cluster administration

* **Cluster bootstrap**

  - [Step 1: prepare cluster virtual machines (Flatcar Linux)](cluster/ignition/)
  - [Step 2: setup external HAProxy load-balancer](cluster/external-lb/)
  - [Step 3: bootstrap the cluster with k0s/k0sctl](cluster/k0s/)

* **Services deployment**

  - [Persistent storage with OpenEBS](deployments/openebs)

## References

- **ArgoCD** : https://github.com/argoproj/argo-cd/
- **Calico** : https://www.tigera.io/project-calico/
- **HAProxy** : https://www.haproxy.com/
- **HAProxy Ingress Controller** : https://github.com/haproxytech/kubernetes-ingress
- **k0s** : https://k0sproject.io/
- **k0sctl** : https://github.com/k0sproject/k0sctl
- **Velero** : https://github.com/vmware-tanzu/velero
