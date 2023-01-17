---
title: Two Pods
permalink: /handson/2
parent: HandsOn exercises
nav_order: 2
---

# HandsOn exercises "Two Pods"

## Goal

This exercise is intended to show you how communication with 2 pods works.

## Steps

1. Create pod 2 with following image `nginxdemos/hello:0.1` and different pod names and the label `app: hello`
2. Create a Service with the name `hello` and the selector for the label of the pods and the type loadbalancer.
3. Get status of resources

   `kubectl get po,svc,ep`

4. Test webapplication throw loadbalancer many times
