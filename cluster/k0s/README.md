### Step 3: bootstrap the cluster with k0s/k0sctl

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
wk8s01   Ready    <none>   108s   v1.23.6+k0s
wk8s02   Ready    <none>   108s   v1.23.6+k0s
wk8s03   Ready    <none>   108s   v1.23.6+k0s
...
```

```shell
$ kubectl get pods -A

NAMESPACE     NAME                                  READY   STATUS    RESTARTS   AGE
kube-system   cilium-4zmlc                          1/1     Running   0          76s
kube-system   cilium-mmjht                          1/1     Running   0          75s
kube-system   cilium-operator-764cc67877-mszrw      1/1     Running   0          79s
kube-system   cilium-operator-764cc67877-p58hw      1/1     Running   0          79s
kube-system   cilium-qp9nv                          1/1     Running   0          75s
kube-system   coredns-8565977d9b-68n6t              1/1     Running   0          79s
kube-system   coredns-8565977d9b-dxxsw              1/1     Running   0          54s
kube-system   csi-nfs-controller-6c79b79bd5-9w7lm   3/3     Running   0          79s
kube-system   csi-nfs-node-dzb25                    3/3     Running   0          75s
kube-system   csi-nfs-node-f987n                    3/3     Running   0          75s
kube-system   csi-nfs-node-mhhr2                    3/3     Running   0          76s
kube-system   konnectivity-agent-28wkw              1/1     Running   0          55s
kube-system   konnectivity-agent-ftqpv              1/1     Running   0          55s
kube-system   konnectivity-agent-mjdfr              1/1     Running   0          55s
kube-system   metrics-server-74c967d8d4-bps4c       1/1     Running   0          73s
...
```

*NOTE : with k0s, the controller nodes and 'control plane pods' are not appearing when retrieving cluster nodes/pods using kubectl command-line because there is no container runtime or kubelet running on controllers by design*

[Return to main page](../../README.md)
