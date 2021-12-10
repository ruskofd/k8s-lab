Various notes on cluster architecture deployment

## Bootstrap the cluster using k0sctl

To bootstrap the cluster, simply use the following command :

```shell
$ k0sctl apply -c ./k8s/k0s-config.yml
```

## HAProxy

**Allow HAProxy to bind to non-local IP addresses when using Keepalived VIP**

```shell
net.ipv4.ip_nonlocal_bind = 1
net.ipv6.ip_nonlocal_bind = 1
```

**Access HAProxy stats page behind SNAT network using LXD proxy device**

```shell
$ lxc config device add lk8s01 haproxy-stats proxy listen=tcp:10.0.1.102:9000 connect=tcp:127.0.0.1:9000
```
