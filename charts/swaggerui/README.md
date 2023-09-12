# Helm Chart for swagger-ui

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Introduction

This [Helm](https://github.com/kubernetes/helm) chart installs [swagger-ui](https://github.com/swagger-ui-api/swagger-ui) in a Kubernetes cluster. This chart is based on work you can find [here](https://github.com/cetic/helm-swagger-ui).

## Prerequisites

- Kubernetes 1.10+
- Helm 3.0.0+

## Installation

### Add Helm repository

```bash
helm repo add chrisfu https://chrisfu.github.io/charts
helm repo update
```

### Configure the chart

The following items can be set via `--set` flag during installation or configured by editing the `values.yaml` directly (need to download the chart first).

#### Configure the way how to expose swagger-ui service:

- **Ingress**: The ingress controller must be installed in the Kubernetes cluster.
- **ClusterIP**: Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster.
- **NodePort**: Exposes the service on each Node’s IP at a static port (the NodePort). You’ll be able to contact the NodePort service, from outside the cluster, by requesting `NodeIP:NodePort`.
- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer.

### Install the chart

Install the swagger-ui helm chart with a release name `my-release`:

```bash
helm install my-release chrisfu/swaggerui
```

## Uninstallation

To uninstall/delete the `my-release` deployment:

```bash
helm uninstall my-release
```

## Configuration

The following table lists the configurable parameters of the swagger-ui chart and the default values.

| Parameter                                                                   | Description                                                                                                        | Default                         |
| --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------| ------------------------------- |
| **Image**                                                                   |
| `image.repository`                                                          | swagger-ui Image name                                                                                              | `swaggerapi/swagger-ui`         |
| `image.tag`                                                                 | swagger-ui Image tag                                                                                               | `v5.6.2`                        |
| `image.pullPolicy`                                                          | swagger-ui Image pull policy                                                                                       | `IfNotPresent`                  |
| `imagePullSecrets`                                                          | list of names of secrets containing docker registry credentials                                                    | `[]`                            |
| **Swagger-UI**                                                              |
| `swaggerui.jsonUrl`                                                         | location of the configuration json file file                                                                       | `http://petstore.swagger.io/v2/swagger.json` |
| **Deployment**                                                              |
| `deployment.replicas`                                                       | Number of replicas                                                                                                 | `1`                             |
| `deployment.extraEnv`                                                       | Additional environment variable                                                                                    | ``                              |
| **Service**                                                                 |
| `service.type`                                                              | Type of service for swagger-ui frontend                                                                            | `ClusterIP`                     |
| `service.port`                                                              | Port to expose service                                                                                             | `8080`                          |
| `service.nodePort`                                                          | Port where the service is reachable                                                                                | `30245`                         |
| `service.clusterIP`                                                         | internal cluster service IP (set to "-" to pass an empty value)                                                    | `nil`                           |
| `service.loadBalancerIP`                                                    | LoadBalancerIP if service type is `LoadBalancer`                                                                   | `nil`                           |
| `service.loadBalancerSourceRanges`                                          | Address that are allowed when svc is `LoadBalancer`                                                                | `[]`                            |
| `service.annotations`                                                       | Service annotations                                                                                                | `{}`                            |
| **Ingress**                                                                 |
| `ingress.enabled`                                                           | Enables Ingress                                                                                                    | `false`                         |
| `ingress.annotations`                                                       | Ingress annotations                                                                                                | `{}`                            |
| `ingress.path`                                                              | Path to access frontend                                                                                            | `/`                             |
| `ingress.hosts`                                                             | Ingress hosts                                                                                                      | `[]`                            |
| `ingress.tls`                                                               | Ingress TLS configuration                                                                                          | `[]`                            |
| **ReadinessProbe**                                                          |
| `readinessProbe`                                                            | Rediness Probe settings                                                                                            | `nil`                           |
| **LivenessProbe**                                                           |
| `livenessProbe.httpGet.path`                                                | Liveness Probe settings                                                                                            | `/`                             |
| `livenessProbe.httpGet.port`                                                | Liveness Probe settings                                                                                            | `http`                          |
| `livenessProbe.initialDelaySeconds`                                         | Liveness Probe settings                                                                                            | `60`                            |
| `livenessProbe.periodSeconds`                                               | Liveness Probe settings                                                                                            | `30`                            |
| `livenessProbe.timeoutSeconds`                                              | Liveness Probe settings                                                                                            | `10`                            |
| **Resources**                                                               |
| `resources`                                                                 | CPU/Memory resource requests/limits                                                                                | `{}`                            |
| **Autoscaling**                                                             |                                                                                                                    |                                 |
| `autoscaling.enabled`                                                       | Enable HPA Autoscaling                                                                                             | `false`                         |
| `autoscaling.minReplicas`                                                   | Minumum count of ReplicaSet pods                                                                                   | `1`                            |
| `autoscaling.maxReplicas`                                                   | Maximum count of ReplicaSet pods                                                                                   | `10`                            |
| `autoscaling.targetCPUUtilizationPercentage`                                | CPU target threshold for scale-up (across all replicas)                                                            | `80`                            |
| `autoscaling.targetMemoryUtilizationPercentage`                             | Memory target threshold for scale-up (across all replicas)                                                         | `80`                            |

## Contributing

Feel free to contribute by making a [pull request](https://github.com/cetic/helm-swagger-ui/pull/new/master).

Please read the official [Contribution Guide](https://github.com/helm/charts/blob/master/CONTRIBUTING.md) from Helm for more information on how you can contribute to this Chart.

## Thanks

Thanks to [Cetic](https://github.com/cetic/helm-swagger-ui) for the original Helm chart, which this one is based on. Minimal changes have been made to support newer versions of Swagger-UI.

## License

[Apache License 2.0](/LICENSE.md)
