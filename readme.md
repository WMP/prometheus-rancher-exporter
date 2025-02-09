![workflow status](https://github.com/David-VTUK/prometheus-rancher-exporter/actions/workflows/test-build-publish.yml/badge.svg) [![Go Report Card](https://goreportcard.com/badge/github.com/david-vtuk/prometheus-rancher-exporter)](https://goreportcard.com/report/github.com/david-vtuk/prometheus-rancher-exporter)

# Unofficial Prometheus Exporter for Rancher

**Note** : This project is not officially supported by Rancher/Suse.

# Quickstart

1. Enable monitoring in the Rancher Management Cluster, aka `local` cluster
2. Apply the manifest from this repo : `kubectl apply -f ./manifests/exporter.yaml`
3. You can set timers by environment variable:
   
   `TIMER_TICKER=10` - how ofter read data, in seconds
   
   `TIMER_GET_LATEST_RANCHER_VERSION=1` - how often get latest rancher version from github, in minutes

# Grafana Dashboards

`./manifests/grafana-dashboard` includes a basic dashboard in JSON format that can be imported into Grafana.  
`./manifests/grafana-dashboard-projects.json` includes a Rancher project-focused dashboard in JSON format that can be imported into Grafana.  
`./manifests/grafana-dashboard-all-cr.json` includes a dynamic dashboard showing counts for all Rancher custom resources (*.cattle.io).  
`./manifests/grafana-dashboard-nodes.json` includes a dynaic dashboard showing global node metadata across all managed clusters (ie Kernel/OS versions, roles, etc)  

# Example Screenshots  

![img.png](img/overview-dashboard.png)
![img.png](img/proj-dashboard.png)
![img.png](img/cr-dashboard.png)
![image](https://github.com/David-VTUK/prometheus-rancher-exporter/assets/5892615/ffae3d27-0980-4781-953e-05014a17a55d)

# Developing

By default, the exporter will use in-cluster authentication via a associated service account

## External cluster config

To test using external authentication via the local `kubeconfig`, set the following environment variable:

```bash
export RANCHER_EXPORTER_EXTERNAL_AUTH=TRUE
```

* `go run main.go`
* Navigate to http://localhost:8080/metrics
