### Step 2: setup external HAProxy load-balancer

When using an highly-available Kubernetes control-plane, you need to setup a load-balancer to define a single point of contact for access to the `controllers`. The load balancer needs to allow and route traffic to each controller through the following ports:

- `6443` (Kubernetes API)
- `8132` (Konnectivity)
- `9443` (Controller Join API)

In my lab, I only use a single HAProxy instance without any redundancy for resource saving reasons. I also use this load-balancer as external load-balancer to access cluster workloads inside the cluster by loadbalancing the traffic to the ingress controllers (HAProxy Ingress Controller in daemonset mode on each of the three nodes).

Firstly, install HAProxy on whatever distribution you like the most, in my case I use Fedora 35 :

```
$ dnf in -y haproxy
```

Then apply the configuration provided here (don't forget to edit IP addresses :)). Once it's done, simply start the HAProxy service :

```
$ systemctl enable --now haproxy
```

You can then check the status of the backend using the HAProxy stats web page : `http://<haproxy address>:9000`
