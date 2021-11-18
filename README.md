# openhab-helm-chart

This is a Helm Chart for an openhab environment running on a k3s raspberry pi cluster.
It will introduce an influxdb storage and a grafana board.


## Precondition

You would need a k3s cluster up and running on your raspberry pi. For storage, the longhorn 
persistence volume manager has to be installed.


## Installing

Use `helm` to install this chart on your raspberry pi k3s cluster:

```
helm upgrade --install oh /Users/dirk/workspace/openhab-helm-chart 
```

Afterwards you should be able to access openhab using your k3s master node ip-address:

```
http://myk3snode:8080
```


## Accessing the Logfiles

You can access the logfiles by simply accessing the openhab pod.
So find out it's name by
```
kubectl get pods
```
and then:
```
kubectl exec --stdin --tty oh-openhab-helm-chart-58f7f9cf89-p7zw8 -- /bin/bash
```


## Getting the grafana admin password

To access the grafana board, you would initially have to discover the admin password to do so:

```
kubectl get secret --namespace default oh-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo 
```
