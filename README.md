<p><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/67/Kubernetes_logo.svg/2560px-Kubernetes_logo.svg.png" alt="k8s-logo" title="k8s" align="top" height=100 /></p>

Various configurations and deployments for my personal Kubernetes lab cluster.

### Bootstrap a cluster

To bootstrap a cluster, simply use the following command :

```shell
$ k0sctl apply -c ./k0s/cluster.yml
```

### Components used

- **Kubernetes distribution** : k0s (with `k0sctl` as deployment tool)
- **CRI** : containerd
- **CNI** : Cilium (configured as `kube-proxy` replacement)
- **CSI** : *TBD*
- **Load Balancer** : MetalLB
- **Ingress Controller** : Traefik

### How-to

* [Kubernetes Without kube-proxy](https://docs.cilium.io/en/v1.10/gettingstarted/kubeproxy-free/)

### References

- k0s : https://k0sproject.io/
- k0sctl : https://github.com/k0sproject/k0sctl
- Cilium : https://cilium.io/
- MetalLB : https://metallb.universe.tf/
- Traefik : https://traefik.io/
