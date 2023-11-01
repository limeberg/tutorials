Network Policies
===


```bash
# create cluster
kind create cluster --config=config.yaml

# create 'test' namespace
kubectl apply -f namespace.yml

# create app pod which we will use to curl from
kubectl apply -f app.yml

# create db pod which we will curl to from app
kubectl apply -f db.yml

```

