# QuakeKube

A Helm chart for QuakeKube is a Kubernetes-ified version of QuakeJS that runs a dedicated Quake 3 server in a Kubernetes Deployment, and then allow clients to connect via QuakeJS in the browser.

Note: This fork has been slightly modified to support [ExternalDNS](https://github.com/kubernetes-sigs/external-dns) on the NodePort service to easily reach the web service.

Install

```
# Add the repo
helm repo add chrisfu https://chrisfu.github.io/chart

# Install
helm install quake --set quakeServer.eula=true chrisfu/quake-kube
```

> Sources https://github.com/criticalstack/quake-kube
> Forked from https://github.com/grahamplata/charts/tree/master/charts/quake-kube
