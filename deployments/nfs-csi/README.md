### Persistent storage with NFS CSI driver

In this homelab, I use the official NFS CSI driver to provide persistent storage in the cluster. 

#### Setup NFS server

Firstly, we need to setup a NFS server. In my case, I use a virtual NFS server hosted inside a virtual machine for simplicity since I don't plan to host "serious" deployments in this cluster. As usual I will use an Ubuntu 22.04 server :

```shell
# apt install -y nfs-kernel-server
```

Once the package is installed, enable the required service on boot (and start it) :

```shell
# systemctl enable --now nfs-kernel-server.service
```

Then, we need to create an **export** for our NFS StorageClass :

```shell
# vim /etc/exports
/filer/k8s/csi  10.0.122.0/24(rw,sync,no_subtree_check)
```

Finally, apply the new NFS exports configuration :

```shell
# exportfs -rav
```

On another machine, you can check your NFS mount is visible :

```shell
# showmount --exports 10.0.122.5
Export list for 10.0.122.5:
/filer/k8s/csi 10.0.122.0/24
```

#### Create NFS StorageClass

Once the NFS server is ready, we only need to deploy a StorageClass in our cluster in order to use the NFS share since the CSI driver is installed during cluster bootstrap phase.

Here is the content of the StorageClass definition :

```YAML
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs-csi
  annotations:
    storageclass.kubernetes.io/is-default-class: true
provisioner: nfs.csi.k8s.io
parameters:
  server: vfiler.svc.home.lab
  share: /filer/k8s/csi
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions:
- nconnect=8
- nfsvers=4.1
```

You can apply it directly :

```shell
$ kubectl apply -f nfs-storageclass.yml
```

