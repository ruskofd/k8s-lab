### HAProxy Kubernetes Ingress Controller

**Deployment informations**

Chart Version : `1.17.11`
App Version : `1.7.3`

**Install with Helm**

* First, add the HAProxy Helm repository :

  ```shell
  $ helm repo add haproxytech https://haproxytech.github.io/helm-charts
  ```

* Then install the Chart with custom values :

  ```shell
  $ helm repo update

  $ helm install kubernetes-ingress haproxytech/kubernetes-ingress --create-namespace --namespace ingress -f chart-values.yml
  ```

[Return to main page](../../README.md)
