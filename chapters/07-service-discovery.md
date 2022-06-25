# Chapter 07: Service Discovery

## A lousy summary

This chapter starts with an introduction of **service discovery**
and builds upon it to discuss the `Service` object in Kubernetes.
It outlines the qualities of a good service discovery software
and lists the shortcomings of using typical DNS based discovery
tool in Kubernetes environment.

The chapter then describe two types of service objects: `ClusterIP`
and `NodePort`. It briefly talks about the `LoadBalancer` type
service object and points out that its functionality is tied to the
cloud providers.

The chapter uncovers the `Endpoint` object to show how services are
affected by failing [`readinessProbe`](05-pods.md#interesting-bits).
It also points out how the Kubernetes system uses service discovery
internally so it does not need to assign `ClusterIP` to every service.

In the end, the chapter gives some pointers on connecting external (on-premise) services to the Kubernetes cluster.

## Interesting Bits

- Service discovery tools tells which process are listening at listening
  at which address for which service.
- Features of a good service discovery software:
  - low latency
  - reliability
- Why DNS cannot be used for service discovery in Kubernetes?
  - Some systems caches the lookup address from the DNS.
    Thus, they don't get updated when a service gets updated.
  - There's a limit on amount and type of information that can be
    returned in a DNS query.
  - When multiple IPs are found for a DNS record, the client takes
    the first one and relies on the DNS server to randomize or
    round-robin the order of record. This is bad for load-balancing.
- Simplest way to create a service object:
  ```
  kubectl expose deployment <deployment-name>
  ```
- A **service** simply gives a name to a **SELECTOR** and specifies
  which port to use to talk to that service. It also assigns a
  **virtual stable IP address** called `ClusterIP`. `ClusterIP` is
  used to load-balance across all the pods of the service.
- Kubernetes provides a DNS service which is managed by Kubernetes itself.
  It provides DNS names for cluster IPs.

  The service DNS names are in the following format
  ```
  <service-name>.<namespace>.svc.<cluster-base-domain>
  ```
  In `alpaca-prod.default.svc.cluster.local`
  - `alpaca-prod` is the service name
  - `default` is the namespace
  - `svc` depicts the type of API object, in this case `Service`
  - `cluster.local` is cluster's base domain name
- `ClusterIP` exposes the service inside the cluster, `NodePort`
  exposes the service outside the cluster.
- `Endpoints` are low-level APIs that allows system and other
  application to use services without creating `ClusterIP` for them.
  For every Service object, Kubernetes creates a buddy Endpoints object
  that contains the IP addresses for that service.

## Did I know?

- Services from the same namespace can be addressed **only**
  with their service name. Services from other namespaces can
  be addressed with `<service-name>.<namespace>`.
- When a service has been exposed with `NodePort` type, all
  the nodes forwards traffic on the port to that service. This
  means if we can reach any node on the cluster, we can reach
  the service.
- Whenever a pod fails the `readinessProbe`, it's IP address
  is removed from the service `Endpoints`.
- It is possible to manually set the `ClusterIP` for a service,
  but it's not allowed to edit the `ClusterIP`. One needs to
  delete and re-create the `Service` object to change the
  `ClusterIP` of a service.
- `ClusterIP` are also available to the pod through the means of
  environment variables. If one wants to rely on environment variables for
  `ClusterIP`, then they will need to deploy services first before
  before creating the pods. Due to this complexity, using DNS
  for getting `ClusterIP` is preferred.

*Note Created: 2022-06-25*
