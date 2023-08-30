## Context in Kubernetes:
A context in Kubernetes refers to a combination of a cluster, a user, and a namespace. It's essentially a set of configurations that determine where and how the kubectl command-line tool interacts with a Kubernetes cluster. Contexts allow you to switch between different clusters, users, and namespaces without having to modify your kubectl commands every time. This is particularly useful when managing multiple clusters or environments.

A context typically includes:
- `Cluster`: The details of the Kubernetes cluster you want to interact with, such as the cluster's server address and credentials.

- `User`: The user credentials (authentication information) used to access the cluster.
- `Namespace`: The default namespace that should be used when interacting with the cluster. This can be overridden in individual commands.

By managing contexts, you can seamlessly switch between different Kubernetes clusters, users, and namespaces without needing to remember or specify the configuration details each time.


```
kubectl config view

kubectl config get-contexts

kubectl config set-context kubesys --namespace=kube-system --user=kubernetes-admin --cluster=<cluster-name>

# for getting kubernetes cluster-name
kubectl config view --minify -o jsonpath='{.clusters[].name}'

kubectl config current-context

kubectl config get-contexts
kubectl config use-context kubesys



```



### Namespace in Kubernetes:
A namespace is a logical partition within a Kubernetes cluster that allows you to group and isolate resources. It provides a way to create separate virtual clusters within a physical cluster, preventing naming collisions and providing resource separation and management.