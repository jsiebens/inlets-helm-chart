# Inlets Helm Chart

[Inlets](https://github.com/inlets/inlets), a Cloud Native Tunnel written in Go, combines a reverse proxy and websocket tunnels to expose your internal and development endpoints to the public Internet via an exit-node.

## Introduction

This chart bootstraps an Inlets deployment, service and ingress on a Kubernetes cluster using the Helm package manager.

### Why?

For larger teams working on projects with webhooks like Stripe and Slack, it can become a little bit expensive when all members have a running exit-node to demo or test their stuff. Inlets is such a lightweight tool, and it can smoothly run in a container. When deployed on a Kubernetes cluster, many Inlets servers can share a single exit-node.

Some cloud providers, like [DigitalOcean](https://www.digitalocean.com/products/kubernetes/) or [Scaleway](https://www.scaleway.com/en/kubernetes-kapsule/) have quite cheap Kubernetes services. (On Scaleway you can get a single node Kubernetes cluster for €7.99/month)

## Prerequisites

An Ingress Controller (nginx-ingress, traefik, ...) up and running in your Kubernetes cluster.

A wildcard DNS (e.g. *.example.com) A record pointing to the public ip adress of your Ingress Controller

## Installing the chart

Add repository to Helm:

```bash
helm repo add inlets TODO
```

You can update the chart repository by running:

```bash
helm repo update
```

Install an Inlets server, e.g.:

```bash
helm install bumblebee inlets/inlets --set inlets.domain example.com --set inlets.token=<your token>
```

## Using the Inlets server

As soon the deployment is ready, and the ingress is picked up by the controller, you can connect to the server with an Inlets client, e.g.:

```bash
export UPSTREAM=http://127.0.0.1:8000

inlets client  \
  --remote=ws://bumblebee.example.com  \
  --token <your token> \
  --upstream $UPSTREAM
```

## Securing the tunnel

Most of the Ingress controllers support SSL termination. At this moment the ingress created by this chart does not support HTTPS / TLS yet.

## Configuration

The following table lists the configurable parameters of the inlets chart and their default values.

Parameter | Description | Default
--- | --- | ---
`inlets.domain` | your domain | 
`inlets.token` | token for authentication | 
`inlets.image.repository` | inlets container image repository | `inlets/inlets`
`inlets.image.tag` | inlets container image tag | `2.7.0`