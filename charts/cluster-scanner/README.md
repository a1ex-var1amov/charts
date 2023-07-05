<!--


DO NOT MODIFY THIS FILE MANUALLY!!

IT'S AUTO-GENERATED vía README.tpl with pre-comit plugin
this is under construction so it must be launched manually

in the project root, run:
$ pre-commit install
$ pre-commit run -a

-->

# Cluster Scanner - [Controlled Availability]

[Sysdig Cluster Scanner](https://docs.sysdig.com/en/docs/sysdig-secure/scanning) features Runtime Image scanning on Kubernetes.
<br/>This chart deploys the Sysdig Cluster Scanner in your Kubernetes cluster.

**NOTE: Sysdig Cluster Scanner is released in Controlled Availability to selected customers. If you would like to use it, please contact your Sysdig Field Representative or our Support.**

## TL;DR;

```
$ helm repo add sysdig https://charts.sysdig.com
$ helm repo update
$ helm upgrade --install sysdig-cluster-scanner sysdig/cluster-scanner \
      --create-namespace -n sysdig --version=0.1.2  \
      --set global.clusterConfig.name=CLUSTER_NAME \
      --set global.sysdig.region=SYSDIG_REGION \
      --set global.sysdig.accessKey=YOUR-KEY-HERE
```

- [Configuration](#configuration)
- [Usages](#usages)
- [Confirm Working Status](#confirm-working-status)
- [Troubleshooting](#troubleshooting)

<br/><br/>

## Introduction

This chart deploys the Sysdig Cluster Scanner as a Deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.


### Prerequisites

- Helm 3
- Sysdig AccessKey


###  Installing the Chart

To install the chart with the release name `cluster-scanner`, run:

```console
$ helm upgrade --install sysdig-cluster-scanner sysdig/cluster-scanner \
       --create-namespace -n sysdig --version=0.1.2 \
       --set global.clusterConfig.name=CLUSTER_NAME \
       --set global.sysdig.region=SYSDIG_REGION \
       --set global.sysdig.accessKey=YOUR-KEY-HERE
```

To find the values:

- YOUR-KEY-HERE: This is the sysdig access key.
- CLUSTER_NAME: The name to be used for the cluster. Make sure it is unique for all your clusters.
- SYSDIG_REGION: The region of the Sysdig Backend to use. E.g.: `us1`, or `eu1`.

The command deploys the Sysdig Cluster Scanner on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`


### Uninstalling the Chart

To uninstall/delete the `cluster-scanner`:

```console
$ helm uninstall sysdig-cluster-scanner -n sysdig
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the `cluster-scanner` chart and their default values.

|                     Parameter                      |                                                                                                                                                                                                       Description                                                                                                                                                                                                       |                    Default                    |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------|
| global.clusterConfig.name                          | The name of the cluster. Make sure to set a unique value for all the clusters being inspected.                                                                                                                                                                                                                                                                                                                          | <code>""</code>                               |
| global.sysdig.accessKey                            | Your Sysdig Agent Access Key                                                                                                                                                                                                                                                                                                                                                                                            | <code>""</code>                               |
| global.sysdig.region                               | Region name for Sysdig. Valid options: `us1`, `us2`, `us3`, `us4`, `eu1`, `au1`. When no region is suitable (e.g. on-premise installations) set the `global.sysdig.apiHost: ""` parameter.                                                                                                                                                                                                                              | <code>"us1"</code>                            |
| global.image.pullSecrets                           | The pull secrets for Cluster Scanner                                                                                                                                                                                                                                                                                                                                                                                    | <code>[]</code>                               |
| global.image.pullPolicy                            | The pull policy for Cluster Scanner                                                                                                                                                                                                                                                                                                                                                                                     | <code>IfNotPresent</code>                     |
| global.loggingLevel                                | Set the logging level to use, useful for troubleshooting. Valid values, sorted by increasing level of verbosity are: `PANIC`, `FATAL`, `ERROR`, `WARN`, `INFO`, `DEBUG`, `TRACE`.                                                                                                                                                                                                                                       | <code>"INFO"</code>                           |
| eveEnabled                                         | Enables Sysdig Eve to retrieve the list of running packages.                                                                                                                                                                                                                                                                                                                                                            | <code>false</code>                            |
| eveIntegrationEnabled                              | Enables the integration with Sysdig Eve. Stores the list of running packages to Sysdig backend. It implies `eveEnabled: true`.                                                                                                                                                                                                                                                                                          | <code>false</code>                            |
| rootNamespace                                      | The namespace to use to retrieve the cluster UID                                                                                                                                                                                                                                                                                                                                                                        | <code>"kube-system"</code>                    |
| replicaCount                                       |                                                                                                                                                                                                                                                                                                                                                                                                                         | <code>2</code>                                |
| scannerMode                                        | The scannerMode of the Cluster Scanner. Supported values are `local` or `multi`. Please refer to docs.sysdig.com for further documentation.                                                                                                                                                                                                                                                                             | <code>"local"</code>                          |
| onPremCompatibilityVersion                         | Optional parameter used to check the compatibility of cluster-scanner component versions with the on-premised backend version. If you are running an on-prem version of the Sysdig backend, set this parameter with the version of Sysdig backend you are using. E.g. if `onPremCompatibilityVersion=6.2`, we ensure that the image tag is < 1.0.0 for both the Runtime Status Integrator and the Image SBOM Extractor. | <code>"6.2"</code>                            |
| sslVerifyCertificate                               | Can be set to false to allow insecure connections to the Sysdig backend, such as for on-premise installs that use self-signed certificates. By default, certificates are always verified.                                                                                                                                                                                                                               | <code>true</code>                             |
| runtimeStatusIntegrator.image.registry             | The image registry to use for the Runtime Status Integrator component of Cluster Scanner                                                                                                                                                                                                                                                                                                                                | <code>quay.io</code>                          |
| runtimeStatusIntegrator.image.repository           | The image repository to use for pulling the Runtime Status Integrator image                                                                                                                                                                                                                                                                                                                                             | <code>sysdig/runtime-status-integrator</code> |
| runtimeStatusIntegrator.image.tag                  |                                                                                                                                                                                                                                                                                                                                                                                                                         | <code>"0.4.2"</code>                          |
| runtimeStatusIntegrator.multiCluster               | When the Cluster Scanner is running in `multi` mode, set the secret name to be used to retrieve the kubeconfig configuration to connect to the clusters to inspect.                                                                                                                                                                                                                                                     | <code></code>                                 |
| runtimeStatusIntegrator.localCluster               | Restrict access to specific Docker secrets when Cluster Scanner is running in `local` mode. The default behavior is listing all secrets. See `values.yaml` for an example. Optional.                                                                                                                                                                                                                                    | <code></code>                                 |
| runtimeStatusIntegrator.ports.metrics              | The port to be used to expose prometheus metrics for the Runtime Status Integrator                                                                                                                                                                                                                                                                                                                                      | <code>25000</code>                            |
| runtimeStatusIntegrator.ports.probes               | The port to be used for healthcheck probes for the Runtime Status Integrator                                                                                                                                                                                                                                                                                                                                            | <code>7000</code>                             |
| runtimeStatusIntegrator.resources.limits.cpu       | Runtime Status Integrator CPU limit per replica                                                                                                                                                                                                                                                                                                                                                                         | <code>"1"</code>                              |
| runtimeStatusIntegrator.resources.limits.memory    | Runtime Status Integrator Memory limit per replica                                                                                                                                                                                                                                                                                                                                                                      | <code>350Mi</code>                            |
| runtimeStatusIntegrator.resources.requests.cpu     | Runtime Status Integrator CPU requests per replica                                                                                                                                                                                                                                                                                                                                                                      | <code>"350m"</code>                           |
| runtimeStatusIntegrator.resources.requests.memory  | Runtime Status Integrator Memory requests per replica                                                                                                                                                                                                                                                                                                                                                                   | <code>350Mi</code>                            |
| runtimeStatusIntegrator.natsJS.user                | The username to be used in the NATS JetStream instance the Runtime Status Integrator is going to start                                                                                                                                                                                                                                                                                                                  | <code>"default-user"</code>                   |
| imageSbomExtractor.image.registry                  | The image registry to use for the Image SBOM Extractor component of Cluster Scanner                                                                                                                                                                                                                                                                                                                                     | <code>quay.io</code>                          |
| imageSbomExtractor.image.repository                | The image repository to use for pulling the Image SBOM Extractor image                                                                                                                                                                                                                                                                                                                                                  | <code>sysdig/image-sbom-extractor</code>      |
| imageSbomExtractor.image.tag                       |                                                                                                                                                                                                                                                                                                                                                                                                                         | <code>"0.4.2"</code>                          |
| imageSbomExtractor.ports.metrics                   | The port to be used to expose prometheus metrics for the Image SBOM Extractor                                                                                                                                                                                                                                                                                                                                           | <code>25001</code>                            |
| imageSbomExtractor.ports.probes                    | The port to be used for healthcheck probes for the Image SBOM Extractor                                                                                                                                                                                                                                                                                                                                                 | <code>7001</code>                             |
| imageSbomExtractor.resources.limits.cpu            | Image SBOM Extractor CPU limit per replica                                                                                                                                                                                                                                                                                                                                                                              | <code>"1"</code>                              |
| imageSbomExtractor.resources.limits.memory         | Image SBOM Extractor Memory limit per replica                                                                                                                                                                                                                                                                                                                                                                           | <code>350Mi</code>                            |
| imageSbomExtractor.resources.requests.cpu          | Image SBOM Extractor CPU requests per replica                                                                                                                                                                                                                                                                                                                                                                           | <code>"150m"</code>                           |
| imageSbomExtractor.resources.requests.memory       | Image SBOM Extractor Memory requests per replica                                                                                                                                                                                                                                                                                                                                                                        | <code>350Mi</code>                            |
| imageSbomExtractor.cache.type                      | The type of cache to use. Allowed values are `local`, `distributed` and `distributed,local`. When specified more than one, the cache precedence will be applied from right to left. Eg: `distributed,local` will try to hit the local one first, than fallback to distributed one (redis) When setting `distributed`, you should also setup redis settings below accordingly with your redis installation.              | <code>"local"</code>                          |
| imageSbomExtractor.cache.local.maxSizeBytes        | The maximum size in bytes of the local cache. By default it is set to 35MB                                                                                                                                                                                                                                                                                                                                              | <code>"36700160"</code>                       |
| imageSbomExtractor.cache.local.maxElementSizeBytes | When using `local` as cache type, restrict the maximum size of elements to be cached. By default it is set to 100KB                                                                                                                                                                                                                                                                                                     | <code>"102400"</code>                         |
| imageSbomExtractor.cache.local.ttl                 | The TTL for items in the local cache. By default it is set to 7 days.                                                                                                                                                                                                                                                                                                                                                   | <code>"168h"</code>                           |
| nameOverride                                       | Chart name override                                                                                                                                                                                                                                                                                                                                                                                                     | <code>""</code>                               |
| fullnameOverride                                   | Chart full name override                                                                                                                                                                                                                                                                                                                                                                                                | <code>""</code>                               |
| serviceAccount.create                              | Specifies whether a service account should be created                                                                                                                                                                                                                                                                                                                                                                   | <code>true</code>                             |
| serviceAccount.annotations                         | Annotations to add to the service account                                                                                                                                                                                                                                                                                                                                                                               | <code>{}</code>                               |
| serviceAccount.name                                | The name of the service account to use. If not set and create is true, a name is generated using the fullname template                                                                                                                                                                                                                                                                                                  | <code>""</code>                               |
| podAnnotations.prometheus.io/scrape                |                                                                                                                                                                                                                                                                                                                                                                                                                         | <code>"true"</code>                           |
| podAnnotations.prometheus.io/path                  |                                                                                                                                                                                                                                                                                                                                                                                                                         | <code>"/metrics"</code>                       |
| podAnnotations.prometheus.io/port                  |                                                                                                                                                                                                                                                                                                                                                                                                                         | <code>"25000"</code>                          |
| podSecurityContext                                 | Set Cluster Scanner pod security context                                                                                                                                                                                                                                                                                                                                                                                | <code>{}</code>                               |
| securityContext                                    | Set Cluster Scanner security context                                                                                                                                                                                                                                                                                                                                                                                    | <code>{}</code>                               |
| selectorLabels                                     | Set Cluster Scanner Selector Labels                                                                                                                                                                                                                                                                                                                                                                                     | <code>{}</code>                               |
| nodeSelector.kubernetes.io/arch                    | Cluster Scanner is only supported on nodes with amd64 architecture                                                                                                                                                                                                                                                                                                                                                      | <code>amd64</code>                            |
| tolerations                                        | Set Cluster Scanner scheduling tolerations                                                                                                                                                                                                                                                                                                                                                                              | <code>[]</code>                               |
| affinity                                           | Set Cluster Scanner affinity                                                                                                                                                                                                                                                                                                                                                                                            | <code>{}</code>                               |


Specify each parameter using the **`--set key=value[,key=value]`** argument to `helm upgrade --install`. For example:

```console
$ helm upgrade --install sysdig-cluster-scanner sysdig/cluster-scanner \
    --create-namespace -n sysdig --version=0.1.2 \
    --set global.sysdig.region="us1"
```

**Alternatively, a YAML file** that specifies the values for the parameters can be provided while
installing the chart. For example:

```console
$ helm upgrade --install sysdig-cluster-scanner sysdig/cluster-scanner \
    --create-namespace -n sysdig --version=0.1.2 \
    --values values.yaml
```

## Running helm unit tests

The sysdiglabs/charts repository uses the following helm unittest plugin: https://github.com/quintush/helm-unittest

You can test the changes to your chart by running the test suites as follows:

```
make test
```

The helm unit tests are in the tests folder. It is recommended to add new tests as new features are added here.

## Troubleshooting

### Q: I need to troubleshoot, any way to switch to `debug` verbose?
A: If you used helm to install, you can edit the helm `values.yaml` to set `global.loggingLevel=DEBUG`
<br/>Alternatively, you can edit the webhook configmap - add the `logging_level=DEBUG` key-value and restart the scanner
```
    $ kubectl edit configmap -n sysdig cluster-scanner
    $ kubectl rollout restart deployment -n sysdig cluster-scanner
```