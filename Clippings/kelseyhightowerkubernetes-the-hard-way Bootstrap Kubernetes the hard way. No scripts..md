---
title: "kelseyhightower/kubernetes-the-hard-way: Bootstrap Kubernetes the hard way. No scripts."
source: https://github.com/kelseyhightower/kubernetes-the-hard-way
author:
  - "[[kelseyhightower]]"
  - "[[Provisioning the CA and Generating TLS Certificates]]"
published:
created: 2025-10-01
description: Bootstrap Kubernetes the hard way. No scripts. Contribute to kelseyhightower/kubernetes-the-hard-way development by creating an account on GitHub.
tags:
  - clippings
  - learning
---
**[kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way)** Public

Bootstrap Kubernetes the hard way. No scripts.

[Apache-2.0 license](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/kelseyhightower/kubernetes-the-hard-way?resume=1)

This tutorial walks you through setting up Kubernetes the hard way. This guide is not for someone looking for a fully automated tool to bring up a Kubernetes cluster. Kubernetes The Hard Way is optimized for learning, which means taking the long route to ensure you understand each task required to bootstrap a Kubernetes cluster.

> The results of this tutorial should not be viewed as production ready, and may receive limited support from the community, but don't let that stop you from learning!

## Copyright

  
This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).

## Target Audience

The target audience for this tutorial is someone who wants to understand the fundamentals of Kubernetes and how the core components fit together.

## Cluster Details

Kubernetes The Hard Way guides you through bootstrapping a basic Kubernetes cluster with all control plane components running on a single node, and two worker nodes, which is enough to learn the core concepts.

Component versions:

- [kubernetes](https://github.com/kubernetes/kubernetes) v1.32.x
- [containerd](https://github.com/containerd/containerd) v2.1.x
- [cni](https://github.com/containernetworking/cni) v1.6.x
- [etcd](https://github.com/etcd-io/etcd) v3.6.x

## Labs

This tutorial requires four (4) ARM64 or AMD64 based virtual or physical machines connected to the same network.

- [Prerequisites](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/01-prerequisites.md)
- [Setting up the Jumpbox](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/02-jumpbox.md)
- [Provisioning Compute Resources](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/03-compute-resources.md)
- [Generating Kubernetes Configuration Files for Authentication](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/05-kubernetes-configuration-files.md)
- [Generating the Data Encryption Config and Key](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/06-data-encryption-keys.md)
- [Bootstrapping the etcd Cluster](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/07-bootstrapping-etcd.md)
- [Bootstrapping the Kubernetes Control Plane](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/08-bootstrapping-kubernetes-controllers.md)
- [Bootstrapping the Kubernetes Worker Nodes](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/09-bootstrapping-kubernetes-workers.md)
- [Configuring kubectl for Remote Access](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/10-configuring-kubectl.md)
- [Provisioning Pod Network Routes](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/11-pod-network-routes.md)
- [Smoke Test](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/12-smoke-test.md)
- [Cleaning Up](https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/13-cleanup.md)

## Releases

[7 tags](https://github.com/kelseyhightower/kubernetes-the-hard-way/tags)

## Packages

No packages published