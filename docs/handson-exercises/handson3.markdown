---
title: Rolling Update
permalink: /handson/3
parent: HandsOn exercises
nav_order: 3
---

# HandsOn exercises "Rolling Update"

## Goal

A deployment should be created and be accessible via a service. After the creation, the first update should be carried out and then rolled back again. the status should be taken into account.

## Steps

1. Cleanup execercises 1 and 2
2. Create deployment `hello` with 2 replicas, with following image `nginxdemos/hello:0.1`.
3. Create a Service with the name `hello` for the deployment `hello`.
4. Update the deployment to the image `nginxdemos/hello:0.2` and test the service during the update process.
5. rollback to the first revision.
