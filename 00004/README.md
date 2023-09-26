Gatekeeper Policy Agent
===

```bash
# download gatekeeper policy agent
curl -o ./gatekeeper/bundle.yml https://raw.githubusercontent.com/open-policy-agent/gatekeeper/v3.13.0/deploy/gatekeeper.yaml

# create cluster with kind
kind create cluster --config=config.yaml

# deploy gatekeeper
kubectl apply -k gatekeeper

# list namespaces and you should see 'gatekeeper-system' in the list
kubectl get ns

# in the gatekeeper-system namespace you should see 4 running pods. the audit pod might have a couple of restarts due to the CRDs not being available initially.
kubectl -n gatekeeper-system get pods

# go ahead and list the CRDs that were just deployed as well
kubectl get crd -l=gatekeeper.sh/system=yes

# create the constraints templates
kubectl apply -k constraints/templates

# create the constraints
kubectl apply -f constraints

# create namespace 'dev' for nginx
kubectl apply -f namespace.yml

# go ahead and deploy nginx-not-valid-image-tag
kubectl apply -k nginx-not-valid-image-tag

# go ahead and deploy nginx-not-valid-labels. this will fail.
kubectl apply -k nginx-not-valid-labels

# go ahead and deploy nginx-valid. this will fail.
kubectl apply -k nginx-valid

# for more examples of different policies go to:
# https://open-policy-agent.github.io/gatekeeper-library/website/validation/allowedrepos
```
