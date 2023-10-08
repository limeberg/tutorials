Secure Your Cluster With Gatekeeper Policy Agent
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

# in the gatekeeper-system namespace you should see 4 running pods.
# the audit pod might have a couple of restarts due to the
# CRDs not being available initially.
kubectl -n gatekeeper-system get pods

# go ahead and list the CRDs that were just deployed as well
kubectl get crd -l=gatekeeper.sh/system=yes

# create the constraints templates
kubectl apply -k constraints/templates

# create the constraints
kubectl apply -f constraints

# create nginx apps in namespace 'dev'
kubectl apply -f nginx

# you will see errors
# 'validation.gatekeeper.sh" denied the request: [disallowed-tags] container <nginx> uses a disallowed tag <nginx:latest>; disallowed tags are ["latest"]'
# 'validation.gatekeeper.sh" denied the request: [required-labels] you must provide labels: {"app.kubernetes.io/name"}'

# for more examples of different policies go to:
# https://open-policy-agent.github.io/gatekeeper-library/website/validation/allowedrepos
```
