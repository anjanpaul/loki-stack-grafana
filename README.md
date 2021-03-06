# Install Grafana Loki with Helm
The Helm installation runs the Grafana Loki cluster as a single binary.

# Prerequisites
Make sure you have Helm installed.

Add Loki’s chart repository to Helm:

```
helm repo add grafana https://grafana.github.io/helm-charts

```

To update the chart repository, run:

```
helm repo update

```

# Deploy Loki Stack (Loki, Promtail, Grafana) with persistent volume claim

```
helm install loki-stack grafana/lokistack --values values.yaml -n loki --create-namespace

```

# You can also use this command insted of writing values.yaml

```
helm upgrade --install loki grafana/loki-stack  --set grafana.enabled=true,prometheus.enabled=true,prometheus.alertmanager.persistentVolume.enabled=false,prometheus.server.persistentVolume.enabled=false,loki.persistence.enabled=true,loki.persistence.storageClassName=standard,loki.persistence.size=5Gi


```

To check loki whether it is deployed or not please run these command
```
helm list
helm list -A
helm list -n loki
kubectl get ns
kubectl -n loki get all

```
For port forwarding use this command:

```
kubectl -n loki port-forward svc/loki-stack-grafana 3000:80

```


