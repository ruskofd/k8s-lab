## Step 1 - prepare cluster virtual machines

Before bootstraping, we need to setup the virtual machines with some tweaks. In my case, I use `LXD` to manage my virtual machines and I use cloud-init to apply the required tweaks on the node's first boot :

```shell
$ lxc launch <vm image> ck8s01 -c limits.cpu=2 -c limits.memory=2048MiB -c cloud-init.user-data="$(</path/to/userdata.yml)" --vm
```

All the required tweaks are located in the cloud-init userdata [file](userdata.yml)

