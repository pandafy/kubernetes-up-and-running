# Chapter 06: Labels and Annotations

## A lousy summary

This chapter discusses about usage of labels and annotations
in Kubernetes. Kubernetes is designed to be a decoupled
system, the relationship between objects are defined through
labels. Annotations are just like labels. They are used to
store additional data (metadata) about an object. Some external
applications can use annotations to store additional data
about the object.

## Interesting Bits

- We can use label selectors in kubectl like following
  ```
  kubectl get pods --selctor="<key>=<value>"
  ```
- Label selectors allow following boolean operations
  - `key=value`
  - `key!=value`
  - `key in (value1, value2)`
  - `key notin (value1, value2)`
  - `key` (key is set)
  - `!key` (key not set)
- In manifests, label selectors are used in the following format
  ```yaml
  selector:
    matchLabels:
      app: alpaca
    matchLabels:
      - {key: ver, operator: In, values: [1, 2]}
  ```

## Did I know?

- Kubernetes uses annotations to keep track of rolling deployments.
- Annotations can be used prototype alpha functionalities in Kubernetes
  instead of creating first class APIs.

  **Anecdote:** Some managed Kubernetes providers uses annotations to
  provide additional features. E.g.
  [annotations for Vultr's Load Balancers](https://github.com/vultr/vultr-cloud-controller-manager/blob/master/docs/load-balancers.md#load-balancers).

*Note Created: 2022-06-25*
