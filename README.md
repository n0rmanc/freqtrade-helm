# Freqtrade Helm Chart

This Helm chart deploys [Freqtrade](https://www.freqtrade.io/) - a free and open source crypto trading bot written in Python.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure (if persistence is required)

## Installing the Chart

To install the chart with the release name `my-freqtrade`:

```bash
# Add the Helm repository
helm repo add freqtrade-helm https://n0rmanc.github.io/freqtrade-helm
helm repo update

# Install the chart (Option 1: Using helm install)
helm install my-freqtrade freqtrade-helm/freqtrade-helm

# Install or upgrade the chart (Option 2: Using helm upgrade)
helm upgrade --install my-freqtrade freqtrade-helm/freqtrade-helm
```

The `--install` flag in the upgrade command ensures that if the release doesn't exist, it will be installed. This is a common pattern for ensuring idempotent deployments.

The command deploys Freqtrade on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `my-freqtrade` deployment:

```bash
helm uninstall my-freqtrade
```

## Parameters

### Common parameters

| Name                | Description                                        | Value           |
|---------------------|----------------------------------------------------|-----------------|
| `nameOverride`      | String to partially override common.names.fullname | `""`            |
| `fullnameOverride`  | String to fully override common.names.fullname     | `""`            |
| `commonLabels`      | Labels to add to all deployed objects              | `{}`            |
| `commonAnnotations` | Annotations to add to all deployed objects         | `{}`            |

### Freqtrade parameters

| Name                | Description                                        | Value           |
|---------------------|----------------------------------------------------|-----------------|
| `image.registry`    | Freqtrade image registry                          | `docker.io`     |
| `image.repository`  | Freqtrade image repository                        | `freqtrade/freqtrade` |
| `image.tag`         | Freqtrade image tag                               | `stable`        |
| `image.pullPolicy`  | Freqtrade image pull policy                       | `IfNotPresent`  |

### Deployment parameters

| Name                       | Description                                                                               | Value           |
|----------------------------|-------------------------------------------------------------------------------------------|-----------------|
| `replicaCount`             | Number of Freqtrade replicas to deploy                                                   | `1`             |
| `resources.limits`         | The resources limits for the Freqtrade container                                         | `{}`            |
| `resources.requests`       | The requested resources for the Freqtrade container                                       | `{}`            |
| `persistence.enabled`      | Enable persistence using Persistent Volume Claims                                         | `false`         |
| `persistence.storageClass` | Persistent Volume storage class                                                           | `""`            |
| `persistence.accessModes`  | Persistent Volume access modes                                                            | `[]`            |
| `persistence.size`         | Persistent Volume size                                                                    | `8Gi`           |

### Exposure parameters

| Name                       | Description                                                                               | Value           |
|----------------------------|-------------------------------------------------------------------------------------------|-----------------|
| `service.type`             | Kubernetes Service type                                                                   | `ClusterIP`     |
| `service.port`             | Service HTTP port                                                                         | `80`            |

## Configuration and installation details

### Persistence

The chart mounts a Persistent Volume for data persistence. If persistence is disabled, an emptyDir volume is used.

### Setting Pod's affinity

This chart allows you to set your custom affinity using the `affinity` parameter.

### Deploying extra resources

There are cases where you may want to deploy extra objects, such as custom resources, ConfigMaps, or Secrets. For covering this case, the chart allows adding the full specification of other objects using the `extraDeploy` parameter.

## License

Copyright &copy; 2024

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.