---
title: Kustomize
permalink: /kustomize
nav_order: 9
---

# Kustomize

## Introduction to Kustomize

- Kustomize helps customizing config files in a template free way.
- Kustomize provides a number of handy methods like generators to make customization easier.
- Kustomize uses patches to introduce environment specific changes on an already existing standard config file without disturbing it.
- Kustomize provides a solution for customizing Kubernetes resource configuration free from templates and DSLs.

Kustomize lets you customize raw, template-free YAML files for multiple purposes, leaving the original YAML untouched and usable as is.

## Usage

In some directory containing your YAML resource files (deployments, services, configmaps, etc.), create a kustomization file.

This file should declare those resources, and any customization to apply to them, e.g. add a common label.

File structure:

```sh
~/someApp
├── deployment.yaml
├── kustomization.yaml
└── service.yaml
```

The resources in this directory could be a fork of someone else’s configuration. If so, you can easily rebase from the source material to capture improvements, because you don’t modify the resources directly.

Manage traditional variants of a configuration - like development, staging and production - using overlays that modify a common base.

File structure:

```sh
~/someApp
├── base
│   ├── deployment.yaml
│   ├── kustomization.yaml
│   └── service.yaml
└── overlays
    ├── development
    │   ├── cpu_count.yaml
    │   ├── kustomization.yaml
    │   └── replica_count.yaml
    └── production
        ├── cpu_count.yaml
        ├── kustomization.yaml
        └── replica_count.yaml
```

## kustomization.yaml

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

namespace: default

bases:
- ../base/test

resources:
- deployment.yaml

configMapGenerator:
- name: app-whatever
  files:
  - myFileName.ini=whatever.ini
- name: app-whatever
  files:
  - myFileName.ini=whatever.ini
  literals:
  - JAVA_HOME=/opt/java/jdk
  - JAVA_TOOL_OPTIONS=-agentlib:hprof

secretGenerator:
- name: app-tls
  files:
  - secret/tls.crt
  - secret/tls.key
  type: "kubernetes.io/tls"
- name: secret-with-annotation
  files:
  - app-config.yaml
  type: Opaque
  options:
    annotations:
      app_config: "true"
    labels:
      app.kubernetes.io/name: "app2"
```

## Deployment command

```bash
kubectl apply -k ./
kustomize build ./ | kubectl apply -f -
```
