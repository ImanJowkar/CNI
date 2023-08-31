# HPA
 HPA stands for Horizontal Pod Autoscaler, and it's a feature in Kubernetes (k8s) that allows you to automatically adjust the number of replica pods in a deployment, replica set, or stateful set based on observed CPU utilization or other custom metrics. The goal of HPA is to ensure that your application can handle varying levels of load while optimizing resource utilization.


Here's how HPA works in Kubernetes:

- `Metrics Collection`: HPA continuously collects metrics from the resource metrics API, which includes CPU utilization and memory usage by default. You can also configure custom metrics based on your application's requirements.

- `Metrics Evaluation`: HPA compares the current metric values to the target metric values you've defined in the HPA configuration. For example, you might specify that you want to keep the CPU utilization at around 50%.

- `Scaling Decision`: Based on the comparison between current and target metrics, HPA calculates whether to scale up or down. If the current metric exceeds the target metric, HPA decides to scale out (increase the number of replicas). If the current metric is below the target, it might decide to scale in (decrease the number of replicas).

- `Replica Adjustment`: If HPA decides scaling is necessary, it updates the desired number of replicas for the targeted deployment, replica set, or stateful set. Kubernetes then takes care of creating or terminating pods to match the desired replica count.


if you want use `hpa` in kubernetes you have to install metric server first.

[install-metric-server](https://github.com/kubernetes-sigs/metrics-server)

Configuring HPA involves creating an HPA resource in your Kubernetes cluster, specifying the target metrics and scaling rules. Here's a simplified example of an HPA YAML configuration:


```
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app-deployment
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50


```


In this example, the HPA named `my-app-hpa` is associated with a Deployment named `my-app-deployment`. It uses CPU utilization as the metric and targets an average utilization of 50%. It's configured to scale between a minimum of 2 replicas and a maximum of 10 replicas.

Keep in mind that while HPA is great for handling traffic variations, it might not be suitable for all types of scaling scenarios. It's important to understand your application's resource usage patterns and choose the appropriate metrics and scaling parameters for your specific needs.