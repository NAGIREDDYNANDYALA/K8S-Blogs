
![shubh-hashnode-blog (2)](https://user-images.githubusercontent.com/69069614/183693849-e54c6c01-163b-46d3-b944-63b27241055e.png)



# What is Pod and Why Kuberenetes use Pods?

Pod is a running process in cluster. It contains one or more container such as docker container. In pod containers are managed as single entity and share the resources. You can have different types of containers in a single pod whether it is related to application or database.

![image](https://user-images.githubusercontent.com/69069614/182211103-440cabac-ebbd-4feb-80d2-36a485d16525.png)

Kuberetes does not run contaiers directly intsead it run the pod and groups the containers and ensures that each of them use same resources and network.
The main purpose of using pods is **Replication.** When containers are grouped together into pod then with replication kubernetes can horizontally scale application as needed. In other words if a single pod is workload increases Kuberentes will make the replicas of it and will deploy to the cluster. This ensures that during heavy workload cluster will perfom effeciently and also by making replicas it provides failure resistence to the cluster.

**Pods in a Kubernetes cluster are used in two main ways :**

**1. Single container Pod**

Single container pod refers to the pod which contains only one container. you can deploy such pod by writing a yaml file. And running the kubectl command

```
apiVersion: v1
kind: Pod
metadata:
  name: webserver
  namespace: websrvr
  labels:
    app: nginx
    tier: front
    version: v1
    env: production
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

Once the yaml file is created save the file let's give name **nginx.yaml** and run the create command to run the file.

```
kubectl create –f nginx.yml
```
It will create a pod with the name of nginx. We can use the describe command along with kubectl to describe the pod.

**2. Multi container Pod**

Multi container pod refers to the pod which contains one or more containers. you can deploy such pod by writing a yaml file. And running the kubectl command.

```
apiVersion: v1
kind: Pod
metadata:
  name: multicontainer-pods
  namespace: multi
  labels:
    app: httpd
    tier: frontend-backend
    version: v1
spec:
  containers:
  - name: web
    image: httpd
    ports:
    - containerPort: 80
  - name: db
    image: mysql
    ports:
    - containerPort: 3306
    env:
    - name: MYSQL_ROOT_PASSWORD
      value: *******
 ```
 
 In the above yaml file, we have created one pod with two containers inside it, one for httpd and the other for MySQL. You can execte the yaml file with kubectl create command.
 

# Namespaces

Namspace are the logical separation for different environments with the help of namespace you can use same resources at a time as they are logically seperated.
you can use any number of namspaces supported in cluster and they have ability to communicate with each other.

**Some of the usecase why to use Namespces :**

- You can separate development, testing, and deployement environment of containerized applications enabling the entire lifecycle to take place on the same cluster.
- With the namespace you can divide the resourcs of the cluster between multile teams.
- Allowing teams or projects to exist in their own virtual clusters without fear of impacting each other’s work.

## There are following initial namspaces in Kubernetes

**1. default**
This is the default namespace for every kubernetes command and every kuberenets resource resides in this defult namespace until new namespace are created the entire cluster resides in default.

**2. Kube-System**
This namespce is used for kuberenets componenes which should be avoided for use.

**3. Kube-Public**
This namespce is automatically created and its for only reserved for cluster usage but it is readable by all users.

## Creating Namespce

Here we are creating two namespces named as NP1 and NP2 like this you can create namespce according to you requirements.

```
apiVersion: v1
kind: Namespace
metadata:
  name: NP1
```
```
apiVersion: v1
kind: Namespace
metadata:
  name: NP2
```

## Deleting Namespce

You can delete namespce by executing below command :

```
kubectl delete ns NP1
```

# Basic Kubectl Commands

- This is use to get all the namespace which are created.
```
kubectl get ns
```

- This command is used for get all the resources which are under default namespce.
```
kubectl get all -n default
```

- With this command you will all the componenets of the cluster.
```
kubectl get all -n kube-system
```

- This is also same command as above but it will display information in detail about the cluster components.
```
kubectl get all -n kube-system -o wide
```

# Community Asked Questions

**1. How many Container can a Pod have**

**Ans :** We can have total 5000 nodes, Total 150000 Pods not more than that and not more than 300000 total containers.
