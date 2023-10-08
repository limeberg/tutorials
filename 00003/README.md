Effortless Deployment of Prometheus-Operator in Just a Few Steps!
===

- [Blog](https://www.limeberg.com/blog/effortless-deployment-of-prometheus-operator-in-just-a-few-steps/) 📖
<!-- - [Youtube 📹](#) -->

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

# port-forward prometheus
kubectl -n o11y port-forward svc/prometheus-operated 9090

# open browser at http://localhost:9090
# go to status -> targets
# you should see 'podMonitor/o11y/prometheus/0 (1/1 up)'
# you are successfully getting metrics from prometheus itself
```