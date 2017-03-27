
## Overview

Slight modifications were made to the official docker image to make it more compatible with kubernetes. 

* explicit setting the `gid` for `fsGroup` security context when mounting persistent volume.
* mapped `nexus.vmoptions` and `nexus.rc` to `bin/conf` directory for compatibility with configmaps.



### Create the namespace

```
kubectl create -f conf/nexus.namespace.yml
```

### Create service

```
kubectl create -f conf/nexus.services.yml
```

### Create runtime configmap

```
kubectl create configmap nexus-runtime --from-file=conf/runtime --namespace=nexus
```


### Create default configmap

```
kubectl create configmap nexus-fabric --from-file=conf/etc/fabric --namespace=nexus
kubectl create configmap nexus-jetty --from-file=conf/etc/jetty --namespace=nexus
kubectl create configmap nexus-karaf --from-file=conf/etc/karaf --namespace=nexus
kubectl create configmap nexus-logback --from-file=conf/etc/logback --namespace=nexus
kubectl create configmap nexus-ssl --from-file=conf/etc/ssl --namespace=nexus
```

### Create persistent disk

```
gcloud compute disks create --size 200GB nexus-storage
```

```
kubectl create -f conf/nexus.persistent.gce.yml
```

## Deploy

```
kubectl create -f conf/nexus.deployment.yml 
```


### First Time Use

* Disable anonymous
* Change admin password
* It is best to remove all registries and create a storage container explicitly for each.