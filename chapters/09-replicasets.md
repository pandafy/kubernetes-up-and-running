# Chapter 09: ReplicaSets

## A lousy summary

This chapter discusses the use of `ReplicaSet` for managing
pods. It explains how `ReplicaSet` empowers building scalable
and redundant services. It also demonstrates how to configure
autoscaling for `ReplicaSet` that is triggered by external
factors (e.g. memory or CPU usage).

## Interesting Bits

- *ReplicaSet* acts like a cluster-wide *Pod* manager which ensures
  that correct numbers of *pods* are running at all times. It enables
  the self-healing capability for the application.
- Kubernetes uses *Reconciliation Loops* to maintain the required
  state of *ReplicaSet* at all times.
- *ReplicaSet* manages *Pod* using label selectors.
- It is possible to do **imperative scaling** using the following command:
  ```
  kubectl scale rs <replicaset-name> --replicas=<desired-number-of-replicas>
  ```
- Autoscaling for *ReplicaSets* can be done using **Horizontal Pod Autoscaling**.
  It allows to autoscale *Pods* based on external factors (e.g. CPU or memory usage).

  E.g.:
  ```
  kubectl autoscale rs <replicaset-name> --min=<minimum-desired-pods> \
          --max=<maximum-desired-pods>
          --cpu-percent=<cpu-percentage-above-which-pods-should-be-scaled-up>
  ```

## Did I know?

- *ReplicaSets* allows to **adopt** exisiting *Pods* and allows
  to **quarantine** a *Pod* of the *ReplicaSet* to be quarantined
  for debugging.
- *Pods* managed by a *ReplicaSet* has `kubernetes.io/created-by`
  annotation. This allows users to check if a *Pod* is being managed
  by a *ReplicaSet*.
- Kubernetes **does not supports vertical scaling**

*Note Created: 2022-06-26*
