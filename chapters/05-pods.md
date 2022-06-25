# Chapter 5: Pods

## A lousy summary

This chapter gives a detailed introduction to Pods -
the atomic unit of work in the Kubernetes cluster. It explains
how to create manifests (configuration) for pods and add
health checks (liveness and readiness probe) for healthy
working of the containers.  It shines light on the resource
management API of Kubernetes whilst explaining the
**utilization metric**. It also introduces the concept of
persistent volumes through `emptyDir` and `hostPath` volumes.

## Interesting Bits

- **process health check** ensures that the main process of the
  application is always running
- **liveness health check** is a health check for application liveness,
  it runs application-specific logic to verify that the application is
  not only running but also functioning properly
- **liveness probe** implements the *liveness health check* which
  has to be configured on every container on the pod.
- **readiness probe** similar to *liveness health check* but determines
  whether a container is ready to serve user requests. Containers that
  fail *readiness checks* are removed from the service load balancer.
- Apart from *HTTP checks*, Kubernetes provides following
  **types of health checks**:
  - opening a TCP socket on the container (useful for database
    and non-HTTP-based API)
  - executing a script on the container
- Kubernetes helps to reach a higher *utilization metric* by putting
  constraints on the container's resources (CPU, memory, GPU, etc.) utilization.
  This is achieved using the following properties:
  1. `spec.containers.resources.requests`: It defines the minimum resources
     required by the container. The container is guaranteed to be allocated this
     much resources.
  2. `spec.containers.resources.limits`: It defines the upper bound for
     system resources. The kernel enforces these limits. E.g.: if a
     container runs out of the allocated memory, the *kubelet* will
     restart the container terminating the running process.

## Did I know?

- It is possible to retrieve logs from the previous instance of the
  container using the `--previous` flag for `kubectl logs` command:
  ```
  kubectl logs <pod-name> --previous
  ```
- Not all containers are required to mount the volumes defined in a
  pod.
- `emptyDir` volumes are scoped to the pod's lifespan, but they can be
  shared between containers on the pod.

*Note Created: 2022-06-12*
