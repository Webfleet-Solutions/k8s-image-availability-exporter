# k8s-image-availability-exporter

## Introduction

This chart bootstraps a [k8s-image-availability-exporter](https://github.com/flant/k8s-image-availability-exporter) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

> [!WARNING]  
> By default, k8s-iae has unconstrained access to **all** secrets in the cluster!

## Prerequisites
  - Kubernetes 1.12+
  - Helm 2+

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
helm repo add webfleet-k8s-iae https://Webfleet-Solutions.github.io/k8s-image-availability-exporter
helm repo update
helm install my-release webfleet-k8s-iae/k8s-image-availability-exporter
```

The command deploys k8s-image-availability-exporter on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

The default installation includes only the deployment, service, and rbac configuration.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables list the configurable parameters of the k8s-image-availability-exporter chart and their default values.

### General
| Parameter | Description | Default |
| ----- | ----------- | ------ |
| `k8sImageAvailabilityExporter.useSecretsForPrivateRepositories` | Give k8s-iae unconstrained access to all secrets in the cluster. This is necessary if there are images that are referenced from private registries, which are deployed in pods, where the pull secret is not defined in `spec.imagePullSecrets` in plaintext but rather in an external secret. This setting only modifies the RBAC rules. | `true` |
| `k8sImageAvailabilityExporter.image.pullPolicy` | Image pull policy to use for the k8s-image-availability-exporter deployment | `IfNotPresent` |
| `k8sImageAvailabilityExporter.image.repository` | Repository to use for the k8s-image-availability-exporter deployment | `ghcr.io/Webfleet-Solutions/k8s-image-availability-exporter` |
| `k8sImageAvailabilityExporter.image.tag` | Tag to use for the k8s-image-availability-exporter deployment | `latest` |
| `k8sImageAvailabilityExporter.replicas` | Number of instances to deploy for a k8s-image-availability-exporter deployment. | `1` |
| `k8sImageAvailabilityExporter.resources` | Resource limits for k8s-image-availability-exporter | `{}` |
| `serviceMonitor.enabled` | Create [Prometheus Operator](https://github.com/coreos/prometheus-operator) serviceMonitor resource | `false` |
| `serviceMonitor.interval` | Scrape interval for serviceMonitor | `15s` |
| `prometheusRule.enabled` | Create [Prometheus Operator](https://github.com/coreos/prometheus-operator) prometheusRule resource | `false` |
| `prometheusRule.defaultGroupsEnabled` | Setup default alerts (works only if prometheusRule.enabled is set to true) | `true` |
| `prometheusRule.additionalGroups` | Additional PrometheusRule groups | `[]` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
helm install my-release k8s-image-availability-exporter --set k8sImageAvailabilityExporter.replicas=2
```

Alternatively, one or more YAML files that specify the values for the above parameters can be provided while installing the chart. For example,

```bash
helm install my-release k8s-image-availability-exporter -f values1.yaml,values2.yaml
```

> **Tip**: You can use the default [values.yaml](values.yaml)
