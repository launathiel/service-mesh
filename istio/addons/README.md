# Telemetry Addons

This directory contains sample deployments of various addons that integrate with Istio. While these applications
are not a part of Istio, they are essential to making the most of Istio's observability features.

The deployments here are meant to quickly get up and running, and are optimized for this case. As a result,
they may not be suitable for production. See below for more info on integrating a production grade version of each
addon.

## Getting started

To quickly deploy all addons:

```shell script
kubectl apply -f addons/
```

Alternatively, you can deploy individual addons:

```shell script
kubectl apply addons/prometheus.yaml
```

## Addons

### Prometheus

[Prometheus](https://prometheus.io/) is an open source monitoring system and time series database.
You can use Prometheus with Istio to record metrics that track the health of Istio and of applications within the service mesh.
You can visualize metrics using tools like [Grafana](#grafana) and [Kiali](#kiali).

For more information about integrating with Prometheus, please see the [Prometheus integration page](https://istio.io/docs/ops/integrations/prometheus/).

### Grafana

[Grafana](http://grafana.com/) is an open source monitoring solution that can be used to configure dashboards for Istio.
You can use Grafana to monitor the health of Istio and of applications within the service mesh.

This sample provides the following dashboards:

* [Mesh Dashboard](https://grafana.com/grafana/dashboards/7639) provides an overview of all services in the mesh.
* [Service Dashboard](https://grafana.com/grafana/dashboards/7636) provides a detailed breakdown of metrics for a service.
* [Workload Dashboard](https://grafana.com/grafana/dashboards/7630) provides a detailed breakdown of metrics for a workload.
* [Performance Dashboard](https://grafana.com/grafana/dashboards/11829) monitors the resource usage of the mesh.
* [Control Plane Dashboard](https://grafana.com/grafana/dashboards/7645) monitors the health and performance of the control plane.
* [WASM Extension Dashboard](https://grafana.com/grafana/dashboards/13277) provides an overview of mesh wide WebAssembly extension runtime and loading state.

For more information about integrating with Grafana, please see the [Grafana integration page](https://istio.io/docs/ops/integrations/grafana/).

### Kiali

[Kiali](https://kiali.io/) is an observability console for Istio with service mesh configuration capabilities.
It helps you to understand the structure of your service mesh by inferring the topology, and also provides the health of your mesh.
Kiali provides detailed metrics, and a basic [Grafana](#grafana) integration is available for advanced queries.
Distributed tracing is provided by integrating [Jaeger](#jaeger).

For more information about using Kiali, see the [Visualizing Your Mesh](https://istio.io/docs/tasks/observability/kiali/) task.