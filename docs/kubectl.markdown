---
title: Kubectl
permalink: /kubectl
nav_order: 7
---

# Kubectl


## Kubectl configuration and usage

### kubectl commands
- `kubectl help` most important command for beginners
- `kubectl version` shows version of kubectl and server of current context
- `kubectl config ...` only configures kubectl, not the k8s server
  - `kubectl config view`
  - `kubectl config current-context`
  - `kubectl config set PROPERTY_NAME PROPERTY_VALUE`
  - `kubectl config use-context CONTEXT_NAME`
  - `kubectl config get-contexts`
  - `kubectl config set-context demo --user minikube --cluster minikube --namespace demo`
  - `kubectl config use-context demo`
- Imperative configuration commands
  - `kubectl run nginx --image nginx` create a deployment
  - `kubectl expose deploy nginx --port=80 --target-port=80 --type NodePort` create a service with type NodePort for deployment nginx
  - `kubectl create pod nginx --image nginx` create kubernetes object
  - `kubectl create -f nginx.yaml` create object of yanl/json-file
  - `kubectl replace -f nginx.yaml` update ...
  - `kubectl delete -f nginx.yaml` delete ...
- Declarative configuration command
  - `kubectl apply -f k8s/` create/update objects of file

link:

- [Kubernetes Object Management](https://kubernetes.io/docs/concepts/overview/object-management-kubectl/overview/)

### get status of Deployments/Pods

- `kubectl get (TYPE [NAME | -l label] | TYPE/NAME ...)`
- `kubectl describe (-f FILENAME | TYPE [NAME_PREFIX | -l label] | TYPE/NAME)`
- `kubectl logs [-f] [-p] POD [-c CONTAINER]`
- `kubectl attach POD -c CONTAINER`
- `kubectl port-forward POD [LOCAL_PORT:]REMOTE_PORT [...[LOCAL_PORT_N:]REMOTE_PORT_N]`
- `kubectl proxy`

### Rolling-Update

- `kubectl edit (RESOURCE/NAME | -f FILENAME)`
- `kubectl apply -f FILENAME`
- `kubectl rollout history TYPE NAME`
- `kubectl rollout status TYPE NAME`
- `kubectl rollout pause TYPE NAME`
- `kubectl rollout resume TYPE NAME`

### Rollback

- `kubectl rollout undo TYPE NAME`
- `kubectl rollout undo TYPE NAME --revision=NUMBER`
