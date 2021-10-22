<p><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/67/Kubernetes_logo.svg/2560px-Kubernetes_logo.svg.png" alt="k8s-logo" title="k8s" align="top" height=100 /></p>

Various configurations and deployments for my personal Kubernetes lab cluster.

* **Operating System** : Ubuntu Server 21.10 *Impish Indri*
* **Kubernetes distribution** : `k0s` 1.22.2 (+ `k0sctl` to deploy the cluster)

## Bootstrap cluster

```shell
$ k0sctl apply -c ./cluster/cluster.yml
```
## How-to

* [Kubernetes Without kube-proxy](https://docs.cilium.io/en/v1.10/gettingstarted/kubeproxy-free/)

## References
* k0s : https://k0sproject.io/
* k0sctl : https://github.com/k0sproject/k0sctl
* Cilium : https://cilium.io/
* MetalLB : https://metallb.universe.tf/
* Traefik : https://traefik.io/
