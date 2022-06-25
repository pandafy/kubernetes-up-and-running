# Chapter 08: HTTP Load Balancing with Ingress

## A lousy summary

This chapter discusses the use of Ingress in Kubernetes.
It points out that there is no default *Ingress Controller*
in Kubernetes. Instead, *Ingress Controllers* are pluggable
in Kubernetes giving users the freedom to use a controller
that suits their needs.

Ingress acts a **traffic cop** that directs incoming request
to the right **upstream** server. It provides abstraction for
configuring **Layer 7** load balancers.

## Interesting Bits

- **Virtual Hosting**: Hosting multiple HTTP sites on the same
  server. Traditionally, it is done with the help of a load
  balancer or a reverse proxy.
- The Ingress object consist of multiple rules that tell the
  Ingress Controller where to route the request.

  These rules can operates on the properties of the request,
  i.e. routing of request can be done based on the `Host` and
  `path` parameters of the request.
- The Ingress object allows following lookups (called `pathType`) on the path:
  - `Exact`
  - `Prefix`
  - `ImplementationSpecific`

  Check [examples in the Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/ingress/#path-types)
  which explains how these `pathType` are enforced.
- It is possible to redirect request to a path to another hostname
  (service). Though this is a discouraged practice as it has
  potential to break applications that relies on absolute paths.
- TLS certificates can be configured directly on the Ingress object.

## Did I know?

- The `Service` object operate at *Layer 4* of the OSI model.
  `Ingress` obejcts operates at *Layer 7* of the OSI model.
- If a path matches multiple rules of an Ingress object,
  precedence is given to **first longest matching path**.
  If a path matches two rules, precedence is given to path
  with `Exact` `pathType`.
- An Ingress Controller can allow to re-write the path in the HTTP
  request. For NGINX Ingress controller, `nginx.ingress.kubernetes.io/
rewrite-target: /` annotation is used.
- A cluster can have multiple Ingress objects. It is the job of the
  *Ingress Controller* to consolidate (merge) these objects
  and create a coherent configuration.

*Note Created: 2022-06-26*
