<p><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/67/Kubernetes_logo.svg/2560px-Kubernetes_logo.svg.png" alt="k8s-logo" title="k8s" align="top" height=100 /></p>

Repository containing all configurations used to deploy my personal Kubernetes lab cluster.

## Cluster design

### Overview

*To be reworked*

### Components

  - **Base OS** : Ubuntu Server 22.04 LTS
  - **Kubernetes distribution** : k0s `v1.23.6+k0s.1`
  - **CRI** : containerd
  - **CNI** : Cilium (kube-proxy free mode)
  - **CSI** : NFS CSI driver for Kubernetes
  - **Ingress Controller** : HAProxy Ingress Controller

### Nodes description

  - 1x **HAProxy external LB** for Control Plane entrypoint and nodes registration (1vCPU/1GB RAM)
  - 3x **Controller** nodes in HA mode with `etcd` cluster embedded (with 2vCPU/2GB RAM each)
  - 5x **Worker** nodes (with 4vCPU/10GB RAM each)

## Cluster administration

* **Cluster bootstrap**

  - [Step 1: prepare cluster virtual machines)](cluster/nodes/)
  - [Step 2: setup external HAProxy load-balancer (control-plane)](cluster/external-lb/)
  - [Step 3: bootstrap the cluster with k0s/k0sctl](cluster/k0s/)

## References

- **Cilium** : https://cilium.io/
- **HAProxy** : https://www.haproxy.com/
- **HAProxy Ingress Controller** : https://github.com/haproxytech/kubernetes-ingress
- **k0s** : https://k0sproject.io/
- **k0sctl** : https://github.com/k0sproject/k0sctl
- **MetalLB** : https://metallb.universe.tf/
- **NFS CSI driver** : https://github.com/kubernetes-csi/csi-driver-nfs
