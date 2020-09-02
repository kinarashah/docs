---
title: CLI with Rancher
weight: 100
---

Interact with Rancher using command line interface (CLI) tools from your workstation.

## Rancher CLI

Follow the steps in [rancher cli](../cli).

Ensure you can run `rancher kubectl get pods` successfully.


## kubectl
Install the `kubectl` utility. See [install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).


Configure kubectl by visiting your cluster in the Rancher Web UI then clicking on `Kubeconfig`, copying contents and putting into your `~/.kube/config` file.

Run `kubectl cluster-info` or `kubectl get pods` successfully.

_**Available as of v2.4.6**_ 

_Requirements_

If admins have [enforced TTL on kubeconfig tokens](../../api/api-tokens/#setting-ttl-on-kubeconfig-tokens), the kubeconfig file requires [rancher cli](../cli) to be present in your PATH when you run `kubectl`. Otherwise, you’ll see error like: 
`Unable to connect to the server: getting credentials: exec: exec: "rancher": executable file not found in $PATH`. 

This feature enables kubectl to authenticate with rancher server and get new kubeconfig token when required. Following auth providers are currently supported: 

1. Local
2. Active Directory
3. FreeIpa, OpenLdap 
4. SAML providers - Ping, Okta, ADFS, Keycloak, Shibboleth 

When you first run kubectl like, `kubectl get pods` - it will ask you to pick an auth provider and login with rancher server. 
The kubeconfig token is cached in the path where you run kubectl under `./.cache/token`. This token is valid till [it expires](../../api/api-tokens/#expiration-period), or [gets deleted from rancher server](../../api/api-tokens/#deleting-tokens) 
Upon expiration, the next `kubectl get pods` will ask you to login with rancher server again. 
