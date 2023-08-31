  Resource Quota is a Kubernetes resource that allows you to specify and enforce limits on resource consumption within a namespace. Resources include things like CPU, memory, and storage. Resource Quotas are used to ensure that individual users or teams within a Kubernetes cluster don't consume more resources than they are allocated, which helps prevent resource contention and ensures fair sharing of resources among different workloads.


### limit a namespace

```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: quota-demo1
  namespace: quota-demo-ns
spec:
  hard:
    pods: "2"
    configmaps: "1"
    limits.memory: "500Mi"

```

above `ResourceQuota`  ensure that no more than 2 pods and 1 config map are created within the `quota-demo-ns` namespace. If the namespace attempts to exceed these limits, Kubernetes will prevent the creation of additional pods or config maps until the resource consumption falls within the specified limits.




