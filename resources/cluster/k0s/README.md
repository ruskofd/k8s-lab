### Bootstrap a cluster with k0s/k0sctl

To bootstrap the cluster, simply use the following `k0sctl` command :

```shell
$ k0sctl apply -c /path/to/k0sctl.yml
```

Once the cluster is deployed, you can retrieve the `kubeconfig` file in order to interact with the cluster :

```shell
$ k0sctl kubeconfig -c /path/to/k0sctl.yml > $HOME/.kube/config
```

[Return to main page](../../README.md)
