# helm-argo-workflows

A Crossplane Configuration package that installs the Argo Workflows Helm chart with a minimal, stable interface.

## Overview

`helm-argo-workflows` renders a single Helm release for Argo Workflows. It exposes only the inputs needed
for chart values, namespace, and release name, keeping the interface stable while allowing full Helm overrides.

## Features

- **Minimal Helm interface**: values and overrideAllValues with stable defaults
- **Predictable naming**: defaults to `<clusterName>-argo-workflows` in the `argo` namespace
- **GitOps friendly**: ships a `.gitops/` deploy chart

## Prerequisites

- Crossplane installed in the cluster
- Crossplane providers:
  - `provider-helm` (>=v1.0.6)
- Crossplane function:
  - `function-auto-ready` (>=v0.6.0)

## Quick Start

```yaml
apiVersion: pkg.crossplane.io/v1
kind: Configuration
metadata:
  name: helm-argo-workflows
spec:
  package: ghcr.io/hops-ops/helm-argo-workflows:latest
```

```yaml
apiVersion: helm.hops.ops.com.ai/v1alpha1
kind: ArgoWorkflows
metadata:
  name: argo-workflows
  namespace: example-env
spec:
  clusterName: example-cluster
  values:
    server:
      enabled: true
    controller:
      metricsConfig:
        enabled: true
```

## Development

```bash
make render
make validate
make test
```
