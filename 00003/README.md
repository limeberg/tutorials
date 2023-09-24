Effortless Deployment of Prometheus-Operator in Just a Few Steps!
===

```sh
# create namespace
kubectl apply -k .

# download prometheus-operator bundle. change version if necessary
curl -o ./prometheus-operator/bundle.yml https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/v0.68.0/bundle.yaml

# deploy prometheus-operator crds and deployment.
# use flag '--server-side' to avoid warning about too long
# annotation names
kubectl apply --server-side -k prometheus-operator

# deploy prometheus 
kubectl apply -k prometheus

# deploy node-exporter
kubectl apply -k node-exporter

# port-forward prometheus
kubectl -n o11y port-forward svc/prometheus-operated 9090

# open browser at http://localhost:9090
# go to status -> targets
# you should seee node-exporter in the list
# do a simple search for metrics data from node-exporter
# e.g 'node_uname_info'
```