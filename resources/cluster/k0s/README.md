## Notes

### Bootstrap the cluster using k0sctl

To bootstrap the cluster, simply use the following `k0sctl` command :

```shell
$ k0sctl apply -c /path/to/k0sctl.yml
```

Once the cluster is deployed, you can retrieve the `kubeconfig` file in order to interact with the cluster :

```shell
$ k0sctl kubeconfig -c /path/to/k0sctl.yml > $HOME/.kube/config
```

### References

- k0s : https://k0sproject.io/
- k0sctl : https://github.com/k0sproject/k0sctl
