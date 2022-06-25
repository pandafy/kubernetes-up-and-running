# Chapter 3: Deploying a Kubernetes Cluster

## A lousy summary

This chapter describes ways to bring up a Kubernetes clusters.
It emphasizes on using a managed Kubernetes service for learning
to avoid headaches that comes with deploying and managing Kubernetes
on bare metal hardcode.

It also gives a glimpse of few essential `components` of a Kubernetes
clusters.

## Interesting Bits

- Kubernetes Components:
  - **Kubernetes Proxy**: It is responsible for routing network traffic to
    load-balanced services. It is present on every *node*.
  - **Kubernetes DNS**: The DNS is used for naming and discovery of the services
    defined in the cluster. A Kubernetes cluster might contain a replicated (`2`)
    deployment of `core-dns`.
  - **Kubernetes UI**: Not all Kubernetes clusters includes a dashboard GUI,
    but it allows to explore the cluster and even create new containers.

## Did I know?

- [**kind** (Kubernetes in Docker)](https://kind.sigs.k8s.io/)

*Note Created: 2022-06-11*
