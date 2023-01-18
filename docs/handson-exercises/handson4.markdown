---
title: Rolling Update without downtime
permalink: /handson/4
parent: HandsOn exercises
nav_order: 4
---

# HandsOn exercises “Rolling Update without downtime”

## Goal

AIn this exercise we want to update the deployment without downtime.

## Steps

1. Add recources and probes to the deployment demo
2. Update the deployment to the image `nginxdemos/hello:0.2` and test the service during the update process.
3. Create a configmap with the file hello.conf and this content

    ```
    server {
        listen 8080;

        root /usr/share/nginx/html;
        try_files /index.html =404;

        expires -1;

        sub_filter_once off;
        sub_filter 'server_hostname' '$hostname';
        sub_filter 'server_address' '$server_addr:$server_port';
        sub_filter 'server_url' '$request_uri';
        sub_filter 'server_date' '$time_local';
        sub_filter 'request_id' '$request_id';
    }
    ```

4. Mount configmap in deployment hello to filepath etc/nginx/conf.d/hello.conf and change port to 8080
