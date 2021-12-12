### Bootstrap a cluster with k0s/k0sctl

To bootstrap the cluster, simply use the following `k0sctl` command :

```shell
$ k0sctl apply -c /path/to/k0sctl.yml
```

Once the cluster is deployed, you can retrieve the `kubeconfig` file in order to interact with the cluster :

```shell
$ k0sctl kubeconfig -c /path/to/k0sctl.yml > $HOME/.kube/config
```

Then, you can check the correct cluster operation using `kubectl` command-line :

```shell
$ kubectl get nodes

NAME     STATUS   ROLES    AGE     VERSION
wk8s01   Ready    <none>   3m30s   v1.22.4+k0s
wk8s02   Ready    <none>   3m30s   v1.22.4+k0s
wk8s03   Ready    <none>   3m30s   v1.22.4+k0s
```

```shell
$ kubectl get pods -A

NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-6d8ccdbf46-j9h74   1/1     Running   0          114s
kube-system   calico-node-2sx9b                          1/1     Running   0          97s
kube-system   calico-node-nnlsd                          1/1     Running   0          98s
kube-system   calico-node-vbdq2                          1/1     Running   0          97s
kube-system   coredns-77b4ff5f78-8krfl                   1/1     Running   0          114s
kube-system   coredns-77b4ff5f78-f2kbq                   1/1     Running   0          84s
kube-system   konnectivity-agent-55kvj                   1/1     Running   0          77s
kube-system   konnectivity-agent-fc5mx                   1/1     Running   0          77s
kube-system   konnectivity-agent-khxl4                   1/1     Running   0          77s
kube-system   kube-proxy-9hnh2                           1/1     Running   0          97s
kube-system   kube-proxy-tjp8m                           1/1     Running   0          97s
kube-system   kube-proxy-w8rsg                           1/1     Running   0          98s
kube-system   metrics-server-5b898fd875-58qgg            1/1     Running   0          103s
```

*NOTE : with k0s, the controller nodes and 'control plane pods' are not appearing when retrieving cluster nodes/pods using kubectl command-line because there is no container runtime or kubelet running on controllers by design*

[Return to main page](../../README.md)
