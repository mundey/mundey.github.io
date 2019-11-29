---
published: false
layout: post
title: Kuberenetes
categories: Kubernetes
tags: devops kubernetes
author: Jags
---

## Kubernetes Lifecycle management
- Setup Cluster
  - Install base
    - Kmaster
    - Kworker
    - Network
  - Initialize Cluster
  - Join Cluster
    - on kmaster
    ````bash
    kubeadm token list
    ````

  - Setup kubectl
    - kubectl talks to k8 api for operations, just like docker command talks to dockerd
    - To manage k8s from local machine, install kubectl
    https://kubernetes.io/docs/tasks/tools/install-kubectl/
    After installing kubectl, do following
    ````bash
    # create in home directory
    mkdir ~/.kube
    scp kmaster:/etc/kubernetes/admin.conf $HOME/.kube/config
    # Ensure config file has 600 permissions
    # Test configuration works
    kubectl cluster-info
    ````

  - (Optional) Setup Dashboard
    https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

- Launch Applications

- Debug

- Monitor

- 