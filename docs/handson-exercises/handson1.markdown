---
title: First Apply
permalink: /handson/1
parent: HandsOn exercises
nav_order: 1
---

# HandsOn exercises "First Apply"

## Goal

We want to create a local KIND-Cluster

## Steps

1. Create kind config kind.yaml with content

   ```yaml
   kind: Cluster
   apiVersion: kind.x-k8s.io/v1alpha4
   nodes:
   - role: control-plane
     extraPortMappings:
     - containerPort: 30101
        hostPort: 30101
        listenAddress: "127.0.0.1"
      - containerPort: 30102
        hostPort: 30102
        listenAddress: "127.0.0.1"
      - containerPort: 30103
        hostPort: 30103
        listenAddress: "127.0.0.1"
      - containerPort: 30104
        hostPort: 30104
        listenAddress: "127.0.0.1"
      - containerPort: 30105
        hostPort: 30105
        listenAddress: "127.0.0.1"
    ```

2. Start Cluster with Kind

   `kind create cluster --config kind.yaml`

2. Create file `nginx.yaml` with following content

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment
   spec:
     selector:
       matchLabels:
         app: nginx
     replicas: 2 # tells deployment to run 2 pods matching the template
     template:
       metadata:
         labels:
           app: nginx
       spec:
         containers:
         - name: nginx
           image: nginx:1.14.2
           ports:
           - containerPort: 80
    ```

3. Check kubectl configuration

   `kubectl version`
   `kubectl get nodes`

4. Apply nginx

   `kubectl apply -f nginx.yaml`

5. Check status

   `kubectl get deployments,pods`

6. Read Logs of container

   `kubectl logs <pod-name>`
