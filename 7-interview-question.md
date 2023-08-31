# Q1. How is Kubernetes different from Docker Swarm?
Kubernetes and Docker Swarm are both container orchestration platforms, but they have some differences in terms of features, architecture, and intended use cases. Here's a simplified comparison:

## Kubernetes:

`Complexity and Scale`: Kubernetes is known for its flexibility and ability to manage very large and complex deployments. It's suitable for enterprises and organizations with complex needs.

`Architecture`: Kubernetes has a more complex architecture with multiple components such as the master node, worker nodes, and various controllers. This allows for more advanced features and fine-grained control.

`Advanced Networking`: Kubernetes offers rich networking features, including support for various network plugins and configurations, which is useful for intricate network setups.

`Ecosystem`: Kubernetes has a larger ecosystem with a wide range of tools, plugins, and third-party integrations available. It's well-suited for organizations looking for a comprehensive solution.

`Declarative Configuration`: Kubernetes focuses on declarative configuration, where you define the desired state of your applications, and Kubernetes works to maintain that state.

## Docker Swarm:

`Simplicity`: Docker Swarm is designed to be more straightforward and user-friendly, making it a good choice for smaller teams or those new to container orchestration.

`Integrated`: Since Docker Swarm is part of the Docker ecosystem, it's tightly integrated with Docker and can be easier to set up if you're already familiar with Docker.

`Built-in Features`: Docker Swarm offers most of the necessary features out of the box, which simplifies setup and configuration. It may not have as many advanced features as Kubernetes, but it covers the basics.

`Scalability`: While Docker Swarm can handle reasonably large deployments, it might not be as well-suited for extremely complex and large-scale environments compared to Kubernetes.

`Orchestration with Familiarity`: If you're already using Docker and want basic orchestration without a steep learning curve, Docker Swarm might be a better fit.

In summary, Kubernetes is often favored for larger and more complex scenarios that require advanced features and extensive scalability. Docker Swarm is a more accessible option, suitable for simpler setups and teams looking for a smoother transition from using Docker containers alone to container orchestration. The choice between the two depends on your specific requirements, existing expertise, and the complexity of your applications.


# k8s components

### Master Components:
* `API Server`: Acts as the control center of the cluster, receiving and processing requests from users, external systems, and internal components.

* `etcd`: A distributed key-value store that stores the configuration data of the cluster. It acts as the "brain" behind Kubernetes, ensuring data consistency and high availability.


* `Controller Manager`: Monitors the desired state of objects in the cluster and takes actions to maintain or correct that state. Examples include the Replication Controller and the Deployment Controller.


* `Scheduler`: Assigns work (pods) to available nodes based on resource requirements, constraints, and various policies.

### Node Components:
* `Kubelet`: Manages and monitors the state of each node in the cluster. It ensures that the containers are running in a Pod and healthy.

* `Kube Proxy`: Maintains network rules on each node to handle communication between pods and services.



### Networking
* `CNI (Container Network Interface)`: Provides a standardized way for networking plugins to integrate with Kubernetes. Various plugins (like Calico, Flannel, etc.) manage the network communication between pods.



### Add-ons

* `DNS`: A DNS server that provides DNS-based service discovery for Kubernetes services.
* `Dashboard`: A web-based user interface for interacting with the cluster.
* `Ingress Controller`: Manages external access to services within the cluster, typically acting as a reverse proxy.



# How to do maintenance activity on the K8 node?
for maintain a kubernetes node, you have to follow below steps:

1. **drain the node**: efore performing maintenance, you should drain the node to gracefully evict all the running pods from the node. The Kubernetes control plane will schedule the evicted pods to other healthy nodes in the cluster
```
 kubectl drain <node_name> –ignore-daemonsets
```

2. **Mark the Node as Unschedulable**: Prevent new pods from being scheduled on the node during maintenance:
```
  kubectl cordon <node_name>
```

3. **Perform Maintenance Tasks**: Perform any required maintenance tasks on the node, such as OS upgrades, kernel updates, hardware replacements, etc


4. **Verify Node Status**:  After the maintenance is completed, verify that the node is back online and functioning correctly.


5. **Uncordon the Node**: Allow the node to accept new pods again:
```
 kubectl uncordon <node_name>
```



# How do we control the resource usage of POD?

1. **Resource Requests and Limits**: Kubernetes allows you to set resource requests and limits for CPU and memory on a per-container basis within a Pod.

    - `Resource Requests`: It specifies the minimum amount of CPU and memory required for a container to run. Kubernetes will use this information for scheduling and determining the amount of resources allocated to a Pod.

    - `Resource Limits`: It specifies the maximum amount of CPU and memory that a container can consume. Kubernetes enforces these limits to prevent a single container from using more resources than specified, which helps in avoiding resource contention.


 2. **Resource Quotas**: Kubernetes allows you to define Resource Quotas at the namespace level to limit the total amount of CPU and memory that can be consumed by all Pods within the namespace. Resource Quotas help prevent resource hogging and ensure a fair distribution of resources among different applications.