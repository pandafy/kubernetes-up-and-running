# Chapter 4: Common `kubectl` Commands

## A lousy summary

This chapter introduces commonly used `kubectl` commands.

## Interesting Bits

- `kubectl top <pods/nodes>` returns the resource utilization by
  pods or nodes. This relies on the *metric* API. This didn't work
  for me on **kind (Kubernetes on Docker)**.
- **namespaces** are analogous to folders that are used to store objects
- **contexts** can be used to manage different clusters or authenticate
  to a cluster with different users
- Port-forwarding of traffic is also possible using the following command
  ```
  kubectl port-forward <pod-name> 8080:80
  kubectl port-forward services/<service-name> 8080:80
  ```
  **Note:** The traffic will be forwarded to only one pod of the service.
  It will not go through the service load balancer.

## Did I know?
- `kubectl` uses the JSONPath query language to select fields in the
  returned object. This means it is possible to query a particular field
  from the object, e.g.:
  ```
  $ kubectl get pods my-pod -o jsonpath --template={.status.podIP}
  ```
- If the container does not have a bash or some other terminal
  available, it is possible to attach to the running process:
  ```
  $ kubectl attach -it <pod-name>
  ```
  Using this, we can send input to the running process, given that
  the process accepts input from STDIN.
- We can also copy files to and from the container using the
  following command:
  ```
  $ kubectl cp <pod-name>:</path/to/remote/file> </path/to/local/file>
  ```

Note Created: 2022-06-12
