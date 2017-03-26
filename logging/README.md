# Bringing up the ES cluster is a manual process

```
kubectl create -f es-discovery-svc.yaml
kubectl create -f es-svc.yaml
kubectl create -f es-master.yaml
```

Wait until es-master deployment is running


```
kubectl create -f es-client.yaml
kubectl create -f es-data-statefulset.yaml
```

Then we can launch kibana

```
kubectl create -f kibana.svc.yaml
kubectl create -f kibana.deployment.yaml
```
