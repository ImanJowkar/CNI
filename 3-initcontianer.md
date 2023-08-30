# init container

An Init Container (short for initialization container) is a concept in containerization and container orchestration systems, such as Kubernetes. It's a type of container that is designed to run and complete before the main application containers within a pod start running. The primary purpose of an Init Container is to perform setup tasks, configuration, and data initialization that need to be completed before the main application containers can operate correctly.

Here are some key points about Init Containers:
- `Order of Execution`: Init Containers are executed in the order they are defined within the pod's configuration. Each Init Container must complete successfully before the next one starts, and all Init Containers must complete before the main application containers start.

- `Use Cases`: Init Containers are often used for tasks such as downloading and extracting data, setting up configuration files, applying database migrations, and other preparatory tasks that the main application needs.

- `Isolation`: Init Containers run in their own dedicated runtime environment and can have their own set of resource requirements and constraints. This isolation ensures that their actions don't interfere with the main application's runtime environment.

- `Networking and Storage`: Init Containers share the same network namespace and storage volumes with the main containers in the same pod. This allows them to access shared resources and prepare the environment for the main application.

- `Error Handling`: If an Init Container fails to complete successfully, Kubernetes retries running it, unless the restartPolicy of the pod is set to Never. This retry mechanism ensures that the environment is properly prepared before the main application containers start.

- `Configuration`: Init Containers are defined alongside the main containers in the pod specification. Each Init Container is a separate container definition with its own image, commands, arguments, and other properties.



```
apiVersion: v1
kind: Service
metadata:
  name: mysvc
  namespace: test
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress-mysql
  namespace: test
  labels:
    app: MyApp
spec:
  selector:
    matchLabels:
      app: MyApp
  template:
    metadata:
      labels:
        app: MyApp
    spec:
      containers:
      - image: mysql:8.0
        name: mysql
        env:
          - name: MYSQL_ROOT_PASSWORD
            value: test
          - name: MYSQL_DATABASE
            value: wordpress
          - name: MYSQL_USER
            value: wordpress
          - name: MYSQL_PASSWORD
            value: password
        ports:
        - containerPort: 3306
          name: mysql

---
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  namespace: test
  labels:
    app.kubernetes.io/name: MyApp
spec:
  containers:
  - name: myapp-container
    image: busybox:1.28
    command: ['sh', '-c', 'echo The app is running! && sleep 3600']
  initContainers:
  - name: init-myservice
    image: busybox:1.28
    command: ['sh', '-c', 'while ! nc -z  mysvc.test.svc.cluster.local 3306; do echo waiting for mysvc; sleep 1; done']
    #command: ['sh', '-c', 'until nslookup mysvc.test.svc.cluster.local; do echo waiting for mysvc; sleep 1; done']

```



# shared direcotry
```

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    run: nginx
  name: nginx-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      run: nginx
  template:
    metadata:
      labels:
        run: nginx

    spec:

      volumes:
      - name: shared-volume
        emptyDir: {}

      initContainers:
      - name: busybox
        image: busybox
        volumeMounts:
        - name: shared-volume
          mountPath: /nginx-data
        command: ["/bin/sh"]
        args: ["-c", "echo '<h1>Hello Kubernetes</h1>' > /nginx-data/index.html"]

      containers:
      - image: nginx
        name: nginx
        volumeMounts:
        - name: shared-volume
          mountPath: /usr/share/nginx/html

```