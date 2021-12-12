### OpenEBS

**Install with Helm**

* First, add the OpenEBS Helm repository :

  ```shell
  $ helm repo add openebs https://openebs.github.io/charts
  ```

* Then install the Chart with custom values in a dedicated namespace :

  ```shell
  $ helm repo update

  $ helm install openebs openebs/openebs --create-namespace --namespace openebs -f chart-values.yml [--version <Chart version> ]
  ```

**Creating cStor storage pools**

We need to create a Kubernetes custom resource called `CStorPoolCluster` by specifying the details of the nodes and the devices on those nodes that must be used to setup `cStor` pools.

* Firstly, retrieve the avaiable block devices in the cluster :

  ```shell
  $ kubectl get bd -n openebs
  
  NAME                                          NODENAME         SIZE          CLAIMSTATE  STATUS   AGE
  blockdevice-01afcdbe3a9c9e3b281c7133b2af1b68  worker-node-3    21474836480   Unclaimed   Active   2m10s
  blockdevice-10ad9f484c299597ed1e126d7b857967  worker-node-1    21474836480   Unclaimed   Active   2m17s
  blockdevice-3ec130dc1aa932eb4c5af1db4d73ea1b  worker-node-2    21474836480   Unclaimed   Active   2m13s
  ```

* Then, create the `CStorPoolCluster` using the `cspc.yml` file located in this folder :

  ```shell
  $ kubectl apply -f cspc.yml
  ```
* Once it's done, you can check the `CStorPoolCluster` status :

  ```shell
  $ kubectl get cspc -n openebs

  NAME                   HEALTHYINSTANCES   PROVISIONEDINSTANCES   DESIREDINSTANCES     AGE
  cstor-disk-pool        3                  3                      3                    2m2s
  ```

  ```shell
  $ kubectl get cspi -n openebs

  NAME                  HOSTNAME             ALLOCATED   FREE     CAPACITY  STATUS   AGE
  cstor-disk-pool-vn92  worker-node-1        60k         9900M    9900M     ONLINE   2m17s
  cstor-disk-pool-al65  worker-node-2        60k         9900M    9900M     ONLINE   2m17s
  cstor-disk-pool-y7pn  worker-node-3        60k         9900M    9900M     ONLINE   2m17s
  ```

**Creating cStor storage classes**

* Create the `StorageClass` (3 replicas) :

  ```shell
  $ kubectl apply -f sc-cstor-replica3.yml
  ```

[Return to main page](../../README.md)
