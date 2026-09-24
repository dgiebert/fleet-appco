# Fleet Examples for AppCo

```yaml
apiVersion: fleet.cattle.io/v1alpha1
kind: GitRepo
metadata:
  name: fleet-appco
  namespace: fleet-default
spec:
  branch: main
  clientSecretName: auth-ssh
  correctDrift: {}
  helmRepoURLRegex: ^(oci|https)://dp\.apps\.rancher\.io(/.*|$)
  helmSecretName: auth-appco
  pollingInterval: 1m0s
  repo: git@github.com:dgiebert/fleet-appco.git
  targets:
    - clusterSelector: {}
---
apiVersion: v1
stringData:
  password: PASSWORD
  username: USERNAME
kind: Secret
metadata:
  name: auth-appco
  namespace: fleet-default
type: kubernetes.io/basic-auth
---
apiVersion: v1
stringData:
  ssh-privatekey: PRIVATE_KEY
  ssh-publickey: PUBLIC_KEY
kind: Secret
metadata:
  name: auth-ssh
  namespace: fleet-default
type: kubernetes.io/ssh-auth
```