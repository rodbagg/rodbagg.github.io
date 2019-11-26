---
layout: page
title: Kubernetes Collector Details
parent: Log Collectors
nav_order: 1
---
<link rel="shortcut icon" type="image/x-icon" href="{{ site.baseurl }}/images/favicon.ico?" >
# KUBERNETES COLLECTOR DETAILS
Zebrium's Kubernetes collector sends logs to Zebrium for automated Anomaly detection.
Our github repository is located [here](https://github.com/zebrium/ze-kubernetes-collector).

# ze-kubernetes-collector
## Features
* Two step deployment using Kubernetes commands
* Sends logs from all Pods/Containers in a Kubernetes clusters
* Runs a single instance of the collector per node in a Kubernetes cluster

## Getting Started
### Installing via kubectl
The commands below install the Zebrium log collector as a Kubernetes DaemonSet. It runs one collector instance on each node in a Kubernetes cluster.

```
kubectl create secret generic zlog-collector-config --from-literal=log-collector-url=YOUR_ZE_API_URL --from-literal=auth-token=YOUR_ZE_API_AUTH_TOKEN
kubectl create -f https://raw.githubusercontent.com/zebrium/ze-kubernetes-collector/master/templates/zlog-collector.yaml
```

After a few minutes, logs should be viewable on Zebrium web UI.

### Uninstalling via kubectl
The commands below will uninstall the Zebrium log collector. This would typically be done prior to installing a newer version of the collector.
```
kubectl delete -f https://raw.githubusercontent.com/zebrium/ze-kubernetes-collector/master/templates/zlog-collector.yaml
kubectl delete secret zlog-collector-config
```
**Note:** You do not have to delete the secret if there is no change in URL and token when installing an upgraded collector.

### Installing via helm
```
helm install --namespace zebrium  --name zlog-collector --set zebrium.deployment=YOUR_DEPLOYMENT_NAME,zebrium.collectorUrl=YOUR_ZE_API_URL,zebrium.authToken=YOUR_ZE_API_AUTH_TOKEN --repo https://raw.githubusercontent.com/zebrium/ze-kubernetes-collector/master/charts zlog-collector
```

### Uninstalling via helm

If you used the "helm install" command to install zlog-collector chart, you should use the following command to delete:
```
helm delete --purge zlog-collector
```

## Configuration
No special configuration is required

### Setup
By default, Zebrium's kubernetes log collector will be deployed to all Nodes in your cluster and collect logs from each container.

Additionally, each log line will have associated meta data from your Kubernetes deployment viewable in the Zebrium UI. This meta data will include:
1. All Kubernetes Identifier tags such as Node, Pod Name and Id, Container Name and Id, Namespace, etc.
2. All Kubernetes Labels
3. All Kubernetes Annotations

## Testing your installation
Once the collector has been deployed in your Kubernetes environment, your logs and anomaly detection will be available in the Zebrium UI.

## Contributors
* Brady Zuo (Zebrium)
