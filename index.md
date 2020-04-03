# Inlets Helm Chart

## Prerequisites

### Ingress controller

Make sure you have an Ingress controller installed on your Kubernetes cluster

### Helm chart repository

With the command `helm version`, make sure that you have:
- Helm v2/v3 [installed](https://helm.sh/docs/using_helm/#installing-helm)

Add this chart repository to Helm:

```bash
helm repo add inlets https://jsiebens.github.io/inlets-helm-chart
```

You can update the chart repository by running:

```bash
helm repo update
```

## Deploy an Inlets server

```bash
helm install subdomain inlets/inlets --set inlets.domain=example.com --set inlets.token=<your-token>
```

As soon the deployment is ready, you can connect to this Inlet server on `subdomain.example.com`