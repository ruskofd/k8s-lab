Various notes on cluster infrastructure deployment.

## Bootstrap the cluster using k0sctl

To bootstrap the cluster, simply use the following `k0sctl` command :

```shell
$ k0sctl apply -c ./bootstrap/cluster.yml
```

## HAProxy

**Allow HAProxy to bind to non-local IP addresses when using Keepalived VIP**

```shell
net.ipv4.ip_nonlocal_bind = 1
net.ipv6.ip_nonlocal_bind = 1
```

## References

- **ArgoCD** : https://github.com/argoproj/argo-cd/
- **HAProxy Ingress Controller** : https://github.com/haproxytech/kubernetes-ingress
- **OpenEBS** :  https://github.com/openebs/openebs
- **Velero** : https://github.com/vmware-tanzu/velero 
