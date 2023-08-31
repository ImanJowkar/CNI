# jobs and cron jobs

"Jobs" and "Cron Jobs" are resources that are used to manage and automate tasks within a Kubernetes cluster. They provide mechanisms to perform tasks in a reliable, scalable, and automated manner.

- `jobs` : 
In Kubernetes, a Job is a resource that manages the execution of a single task to completion. It ensures that a certain number of pods successfully complete the task before considering the job done. If a pod fails, the job controller creates new pods to replace the failed ones, maintaining the desired number of successfully completed tasks. Jobs are useful for executing batch processes, data processing, and one-off tasks that don't need to be repeated.

- `Cron Jobs`:
Cron Jobs in Kubernetes provide a way to schedule and automate recurring tasks similar to traditional cron jobs in Unix-like systems. A Cron Job resource allows you to specify a schedule in the form of a cron expression, which defines when the task should run (e.g., every hour, every day at a specific time). The Cron Job controller in Kubernetes ensures that the defined task (usually a pod running a container) is created and executed based on the specified schedule.
Cron Jobs are helpful for automating repetitive tasks like backups, data synchronization, and cleanup activities within a Kubernetes environment.

In summary, in the context of Kubernetes:

`Jobs` manage the execution of a single task to completion, ensuring a specified number of successful completions.


`Cron Jobs` automate recurring tasks by scheduling them based on a cron expression, similar to traditional cron jobs in Unix-like systems.




## jobs
```
apiVersion: batch/v1
kind: Job
metadata:
  name: helloworld
spec:
  template:
    spec:
      containers:
      - name: busybox
        image: busybox
        command: ["echo", "Hello Kubernetes!!!"]
      restartPolicy: Never

```

if the jobs exit code doesn't equal to `0` , the jobs repeat again until the procces exit with `0` exit code.

if you delete the pod before the job complete, the jobs run another pod until the procces inside the pod exit with `0` exit code.

if you want to run job more than one time: 
```
apiVersion: batch/v1
kind: Job
metadata:
  name: helloworld
spec:
  completions: 2
  # parallelism: 2
  backoffLimit: 2
  template:
    spec:
      containers:
      - name: busybox
        image: busybox
        command: ["ech", "Hello Kubernetes!!!"]
      restartPolicy: Never

```



## Cronjobs

```
apiVersion: batch/v1
kind: CronJob
metadata:
  name: helloworld-cron
spec:
  schedule: "* * * * *"
  successfulJobsHistoryLimit: 5
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: busybox
            image: busybox
            command: ["echo", "Hello Kubernetes!!!"]
          restartPolicy: Never
```


# delete jobs after completion
you have to add in `/etc/kubernetes/manifest/kube-apiserver.yaml` 

```
- --feature-gates=TTLAfterFinished=true

```