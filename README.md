# vault-controller

This repo contains CRDs and a custom Vault Controller which configures Vault.
This has been tested/validated to work in Kubernetes v1.14.7, running on AWS
EKS.

## Vault CRDs

- VaultPolicy: This resource defines the token policy that needs to be
  configured for a token.

- VaultRole: This resource defines a Vault role and associates a policy to the
  role.

- VaultAuthBackend: This resource configures a Vault auth backend.

- VaultAudit: This resource configures the Vault audit policy.

- VaultSecretEngine: This resouce configures a Vault secret engine.

## Vault Controller

- The controller keeeps a watch on the CRDs and (re)configures them when it is
  notified of a change by the Kubernetes API server.

## Tests

- The `crds/tests` directory contains sample custom resources which can be applied
  to the cluster after applying the CRDs to check if the schemas are valid or
  not.

### Testing locally

Note: `minikube` has issues running over VPN! I have used
[kind](https://github.com/kubernetes-sigs/kind). Install it on Mac using
`brew install kind` and `kind create cluster  --image kindest/node:v1.14.6`,
or use the local Kubernetes cluster bundled with `Docker for Mac`.

- Apply the CRDs using `kubectl --context=docker-desktop apply -f <filename>`
- kubectl --context=docker-desktop api-resources | grep -e vault -e NAME
- kubectl --context=docker-desktop api-versions | grep vault
- Apply the CRDs' test resources to validate the definitions.
- Disable/stop the local k8s cluster


TODO:
- revisit shortNames: they seem confusing