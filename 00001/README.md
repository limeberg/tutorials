Sign and Verify Containers With Ease
===

- [Blog](https://www.limeberg.com/blog/sign-and-verify-containers-with-ease/) 📖
<!-- - [Youtube 📹](#) -->

```sh
# build the container.
docker build -t <registry-name>/<repo-name>:<tag> .

# push container
docker push <registry-name>/<repo-name>:<tag>

# sign the container
cosign sign <registry-name>/<repo-name>:<tag>

# verify container signature
cosign verify \
  --certificate-identity <name@example.com> \
  --certificate-oidc-issuer https://accounts.google.com \
  <registry-name>/<repo-name>:<tag>

# if you want to use self managed keys instead of keyless signing

# generate keypair - keys will be created in the current directory
cosign generate-key-pair

# sign the container with the private key
cosign sign --key cosign.key <registry-name>/<repo-name>:<tag>

# verify the container signature with the public key
cosign verify --key cosign.pub <registry-name>/<repo-name>:<tag>
```