Sign and Verify Containers With Ease
===

```sh

# add signature policy
crio --signature-policy <policy-file-json>

# add signature to specific namespaces
crio --signature-policy <policy-file-json> --signature-policy-dir <policy-dir>

# link to policy spec
# https://github.com/containers/image/blob/main/docs/containers-policy.json.5.md
```