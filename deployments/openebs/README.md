### Persistent storage with OpenEBS

**Install with Helm**

*In this lab, OpenEBS is deployed during cluster bootstrap using k0s Helm Charts deployer.*

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

We need to create a Kubernetes custom resource called `CStorPoolCluster` (since we specify the `cstor` engine during cluster bootstrap) by specifying the details of the nodes and the devices on those nodes that must be used to setup `cStor` pools.

* Firstly, retrieve the avaiable block devices in the cluster :

  ```shell
  $ kubectl get bd -n storage
  NAME                                           NODENAME   SIZE           CLAIMSTATE   STATUS   AGE
  blockdevice-28623d214887d16d2e3dcee4b86c5667   wk8s01     161060208128   Unclaimed    Active   7m48s
  blockdevice-7f7f241d407732b62de1696981fd83b0   wk8s02     161060208128   Unclaimed    Active   7m49s
  blockdevice-d62115fac37354ef8af612b973e24d52   wk8s03     161060208128   Unclaimed    Active   7m21s
  ```

* Then, create the `CStorPoolCluster` using the `cspc.yml` file model located in this folder (don't forget to edit block devices names !) :

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
  cstor-disk-pool-vn92  wk8s01               60k         9900M    9900M     ONLINE   2m17s
  cstor-disk-pool-al65  wk8s02               60k         9900M    9900M     ONLINE   2m17s
  cstor-disk-pool-y7pn  wk8s03               60k         9900M    9900M     ONLINE   2m17s
  ```

**Creating cStor storage classes**

* Create the `StorageClass` (3 replicas) :

  ```shell
  $ kubectl apply -f sc-cstor-replica3.yml
  ```

[Return to main page](../../README.md)

