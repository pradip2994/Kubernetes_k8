![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 001](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/75e23386-2aed-4bf2-8d33-ad66ee08e026)



# Install minikube
## If you are using an EC2 instance take t2.medium instance.

## For installation, you can Visit <https://minikube.sigs.k8s.io/docs/start/> 

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 005](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/44816da3-1b50-4136-8cc7-a90e8516d1b5)



### Installing minikube

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 006](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/0696f8dc-a8f4-48c4-945c-d164db24366f)



First you need to **install Docker** on your machine.

```
$sudo usermod -aG docker $USER

$minikube start --driver=docker
```
Once minikube start finishes, run the command below to check the status of the cluster:

```
$minikube status
```

### Install kubectl

**Kubectl** is a command-line tool used for interacting with Kubernetes clusters. It is the primary and official command-line interface (CLI) for managing and controlling Kubernetes resources and clusters. 

```
$sudo snap install kubectl --classic

$kubectl version
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 007](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/66658043-2202-43a9-a365-e56834cf6b6b)

```
$kubectl get nodes
```

**kubectl get nodes** command is used to retrieve information about the nodes (machines) that form the cluster in your Kubernetes environment. When you run this command, you'll receive a list of all the nodes in your Kubernetes cluster, along with details about their NAME, STATUS, ROLES, AGE, VERSION.

**NAME** :  lists the names of the nodes in the cluster.

**STATUS**:  indicates the current status of each node, such as "Ready" or "NotReady." A "Ready" node is healthy and can accept workloads.

**ROLES**:  can specify roles like "master" or "worker" .

**AGE**:  shows how long each node has been part of the cluster.

**VERSION**:  displays the Kubernetes version running on each node.

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 008](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/b681a2ad-d877-4f48-9be0-5189e22059da)


## Create a folder, inside the folder create a pod.yaml file for nginx.

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 009](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/2b45eca3-d336-4679-be58-3a0b83b9eca6)


Create a pod using pod.yaml file use command:

```
$kubectl create -f pod.yaml
```

You will see that pod is created.

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 010](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/90876d3a-c97b-46d7-95ef-3f6f8a2349d0)


Create pod using command 

$Kubectl apply -f <file_name>
```
$kubectl apply -f pod.yaml
```

You can see that nginx pod is created and running

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 011](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/f753a52b-a60a-41b0-b0b1-cc670e17b49f)


To check list of pods:

```
$kubectl get pods
```
To display entire details of the pods

```
$kubectl get pods -o wide
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 012](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/858f7882-ef56-4653-82eb-97eb1cf6bd80)


Minikube ssh command allows you to access the virtual machine (VM) created by Minikube, which is running the Kubernetes cluster, via a secure shell (SSH) connection. This command is useful for debugging or inspecting the cluster and its components directly on the VM.

```
$minikube ssh
```
Then you will do 
```
curl <ip_address>
```
you can see that the application is running. 

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 013](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/7fb8ad7d-226c-4995-8718-e1dfe1c5a387)


If you want to delete pod use command **kubectl delete pod <pod_name>**

```
$kubectl delete pod nginx
```

## Imp. Q.1. How to debug pods, if there are any application issues in kubernetes?

Using command kubectl describe pod <name\_of\_the \_pod> and kubectl logs <pod>
Example: **kubectl describe pod nginx** and **kubectl logs nginx**

```
kubectl describe pod <name_of_the_pod>
```
Using this you will get the status of everything inside the pod, including whether the pod is currently running, if there are errors within the pod, what those errors are, and any issues with the pod. 

```
$kubectl describe pod nginx
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 014](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/23990f0b-ec6e-4471-9e24-09445d09e8dd)


```
$kubectl logs nginx
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 015](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/008bf89d-b3f6-4895-9741-b584ee06c719)



## Difference between Container, Pods, and Deployments

In Docker, we run containers by providing specifications on the command line. However, Kubernetes takes a different approach. Instead of specifying everything on the command line, Kubernetes streamlines the process and introduces an enterprise-level model. With Kubernetes, you can create YAML manifests to define all the necessary details, such as container images, ports, volumes, and networking, that we typically specify using Docker CLI commands.

A "pod.yaml" manifest serves as a running specification like a Docker container. It's essentially a set of parameters required to run containers. The key difference is that a pod can host one or multiple containers. So, within a pod, you have the flexibility to create either a single container or multiple containers.

Now, what is a deployment in Kubernetes? Kubernetes offers features that are crucial for transitioning from a container platform to Kubernetes. Two of the most important features are auto-healing and auto-scaling. However, pods alone lack these capabilities. They merely provide a YAML specification for running your containers, and that's it.

Auto-scaling and auto-healing are accomplished using deployments in Kubernetes. If you need to achieve zero-downtime deployments, deployments are the way to go. When you deploy using a deployment, it starts by creating replica sets, which are controllers responsible for managing pods. This ensures that the desired number of pods is rolled out smoothly.

###Kubernetes Deployments

A Deployment provides a configuration for updates to Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new replicas for scaling or to remove existing Deployments and adopt all their resources with new Deployments.

**Replica Sets**: It is a resource which ensures that a specified number of pod replicas are running and maintained at all times within a Kubernetes cluster. It is designed to ensure the availability and scalability of pod replicas within a cluster.


![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 016](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/02401e15-d4a8-484c-a853-c3a477d193a4)



Example, Suppose a user has defined two replicas in deployment. The Deployment will create two pods. What a ReplicaSet will do is ensure that these two pods maintain the desired state of resources. It is a Kubernetes controller that implements the autoscaling features for your pods.

## Create one Deployment file to deploy nginx with"Auto-healing" and "Auto-Scaling" feature

**Create a file deployment.yaml**

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 017](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/a6eb247f-6236-4b97-836c-729632344792)


**apiVersion**: apps/v1: This line specifies the API version of Kubernetes that the resource definition is using.

**kind**: Deployment: This line specifies the type of Kubernetes resource being defined, which is a Deployment.

**metadata**: This section contains metadata about the Deployment itself, such as its name and labels.

**name**: nginx-deployment: This sets the name of the Deployment to "nginx-deployment."

**labels**: Labels are key-value pairs used to tag and categorize resources. In this case, the Deployment is given a label "app: nginx."

**spec**: This section defines the desired state of the Deployment.

**replicas**: 3: This specifies that the Deployment should maintain three replicas (three instances) of the Nginx application. If there are fewer than three replicas running, the Deployment controller will create additional replicas to reach this desired state.

**selector**: This is used to select which Pods should be managed by this Deployment.

**matchLabels**: This selector specifies that the Deployment should manage Pods with the label "app: nginx." It ensures that only Pods with this label are controlled by this Deployment.

**template**: This section defines the template for creating new Pods controlled by this Deployment.

**metadata**: Similar to the metadata section for the Deployment itself, this metadata section is used to set labels for the Pods created by this template. In this case, the Pods will also be labeled with "app: nginx."

**spec**: This section specifies the configuration for the Pods created by the template.

**containers**: This is an array that can contain one or more container definitions to run within the Pod.

**name**: nginx: This sets the name of the container to "nginx."

**image**: nginx:1.14.2: This specifies the Docker image to use for the Nginx container. It uses the Nginx image with version 1.14.2.

**ports**: This section is used to specify the ports that should be exposed by the container.

**containerPort**: 80: This sets the container to listen on port 80, which is the default HTTP port used by Nginx.


**Apply the deployment** 

kubectl apply -f <file_name>
```
$kubectl apply -f deployment.yaml
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 018](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/eaf22e18-7bc7-4ec7-96e9-65526c98a849)

kubectl get pods will list and display information about pods.

```
$kubectl get pods
```
kubectl get deploy will list and display information about deployments.

```
$kubectl get deploy
```
kubectl get rs command will display a table with information about each ReplicaSet, including their names, desired replica count, current replica count, age, and labels.

```
$kubectl get rs 
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 019](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/3b5b368f-369e-4dd8-8431-19f777660981)


kubectl get pods -w command is used to list pods in a Kubernetes cluster and watch for updates in real-time. 

```
$Kubectl get pods -w
```

Kubernetes provides auto-scaling and auto-healing capabilities. As you can see in the image above, when I deleted one pod, a new pod was created automatically.

kubectl get all is used in Kubernetes to retrieve information about various resources such as pods, services, deployments in particular namespace.

```
$kubectl get all
```

## Kubernetes Services

Services are responsible for providing a stable network endpoint (IP address and port) for a set of Pods that match a certain label selector. They act as a load balancer or routing layer, directing incoming traffic to one of the matching Pods based on the Service's configuration.

Lets understand in simple words, Imagine you have a bunch of computers (Pods) that run your website or app. Sometimes, these computers go up and down. But you want your website to always be available and reachable.

That's where Kubernetes Services come in. They're like the traffic police for your computers. They give your website a special address (like a phone number) that never changes, even if some computers are hiding or new ones pop up.

Let's understand it how it works:

You define a Kubernetes Service and specify a label selector in its configuration. The Service continuously monitors the cluster for Pods that have labels matching the selector. When a new Pod is created with the matching labels or an existing Pod's labels are updated to match, the Service automatically includes it in its pool of endpoints. When external or internal clients (like other Pods in the cluster) access the Service using its IP address and port, the Service forwards the traffic to one of the Pods that match the label selector.

Types of Services are:

1) ClusterIP, 
1) NodePort, 
1) LoadBalancer, 
1) ExternalName, 
1) Headless Service.

**ClusterIP**: This is the default type of Service. It exposes the Service only within the cluster. It assigns a stable internal IP address to the Service, and other Pods within the cluster can access it using this IP address and port.

**NodePort:** It allows applications to access inside an organization, anybody who has an access to worker notes only they can have access to applications.

**LoadBalancer**: This service will expose your application to the external world. This is suitable for scenarios where you need to distribute traffic from outside the cluster across multiple nodes running the Service. It's commonly used in cloud environments like AWS, Azure, and Google Cloud Platform (GCP).

**ExternalName:** This type of Service maps the Service to a DNS name. It's used when you want to provide a stable DNS name for an external resource, typically a service running outside the cluster.

**Headless Service**: A Headless Service is used when you don't need a stable cluster IP or load balancing.

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 020](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/59ba5095-078e-4113-b92a-fa697f8c352f)



## ClusterIP Service for accessing the todo-app from within the cluster

Create deployment file, todo_app_deployment.yaml

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 021](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/f5a44078-51ca-4b4f-aa65-1c729c1c3e6c)


Create ClusterIP service,  service_clusterip.yaml


![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 022](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/dfac4625-3084-4b07-96d4-1408126282cc)


Service is named **todo-app-clusterip** and is of type **ClusterIP**. The selector **app: todo** is used to determine which Pods to associate with the Service. The Service has a single port, **80**, which is mapped to the target port **8000** on the Pods.

Then apply the ClusterIP Service definition using the 

```
$kubectl apply -f service_clusterip.yaml
```
Then to get the IP address of the ClusterIP Service:

```
$kubectl get svc
```
Now ssh to minikube, minikube ssh command allows you to access the virtual machine (VM) created by Minikube**.**

```
$minikube ssh
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 023](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/5bf557aa-03d7-4d23-ba06-760f9770daf3)


Make a curl request to the ClusterIP Service using its IP address:

```
$curl -L <cluster-ip>:<service-port>
```

You should see the response from the todo-app-clusterip

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 024](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/5727f25e-1432-42cd-9c71-15ec168f47f1)

## NodePort Service for accessing the todo-app from outside the cluster

Create nodeport service, service_nodeports.yaml 

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 025](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/ca596856-1c34-41c3-affc-a576b65a0590)


Service type is set to **NodePort**. This section defines the port mapping for the Service. The Service will listen on port **8000** and forward traffic to the target port **8000** on the pods. Additionally, a **nodePort** is defined as **30007**, which will make the Service accessible from outside the cluster.

Then apply the Service definition using below command

```
$kubectl apply -f service_nodeports.yaml
```

The kubectl get svc command is used to list Services in a Kubernetes cluster. 

```
$kubectl get svc
```

Then type minikube ip command to retrieve the IP address of the Minikube cluster.

```
$minikube ip
```
Then access the todo-app using the Service’s IP and Port:

```
curl -L <service-ip>:<service-port>
```
You should see the response from the todo-app-nodeport.

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 026](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/cba2d379-7ed9-4415-967c-f591be9b9ae7)


## LoadBalancer Service for accessing the todo-app from outside the cluster

Create load balancer service, service_loadbalancer.yaml

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 027](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/13f7179d-d881-4dba-a324-5b5e4f4fd809)


Service is named **todo-app-lb** and is of type **LoadBalancer**. The selector **app: todo** is used to determine which Pods to associate with the Service.

Then apply the LoadBalancer Service definition using the

```
$kubectl apply -f service_loadbalancer.yml

$kubectl get svc

$minikube service list
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 028](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/2ea1403d-5d21-4324-92cb-f1a66e5ef63b)


Access the todo-app from outside the cluster using the LoadBalancer IP and the exposed port:

```
curl -L <load-balancer-ip>:<service-port>
```

You should see the response from the todo-app.

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 029](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/2c90cc10-8e07-44c4-950b-467699b95ce6)


## Kubernetes Ingress

Before moving to the ingress, let's understand why Ingress were introduced. Two problems were faced before when we were using load balancers type, Kubernetes load balancer were there but load balancer were missing below capabilities.

1) It was not supporting enterprising level balancing such as sticky session, black listing white listing domain, security etc.
1) Cloud providers are charging for each of the service types. If there are thousands of service types then they will charge you for 1000 of load balancers static public addresses.

So, these are the two problems facing the Kubernetes before ingress comes into the picture.



Ingress is of no use without an ingress controller. **Ingress Controller** is a load balancer. To make use of Ingress resources, you need an** Ingress controller deployed in your cluster. An Ingress controller is a software component responsible for implementing the Ingress rules by configuring the underlying load balancer or reverse proxy. Popular Ingress controllers include Nginx Ingress Controller, Traefik, and HAProxy Ingress.

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 030](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/bae900c9-6956-44e7-9515-16f7cb91ff9d)


**Ingress** is a configuration that helps manage and control the access to your applications from the outside world. It provides a way to define rules for routing external traffic to different services based on criteria such as hostnames, paths, and HTTP methods. Ingress is essential for setting up HTTP and HTTPS (TLS/SSL) routing for your applications.

In simple terms, Ingress in Kubernetes is like the main entrance and guide for external web traffic to reach different services or applications inside your cluster.

Lets understand in a more simple way, Imagine you have a big building with many rooms, and you want people from outside to visit different rooms, like a museum with different exhibitions. In Kubernetes, Ingress is like the main entrance and a map for visitors to find the rooms they want to visit.

**Create an ingress.yaml file.**

Then apply, 

```
$kubectl apply -f ingress.yaml

$kubectl get ingress
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 031](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/2204aacf-59e6-49e1-91f8-58940b1284eb)


**apiVersion and kind**: These fields specify the API version and resource kind. In this case, it's using the networking.k8s.io/v1 API version and defines an Ingress resource.

**metadata**: This section contains metadata about the Ingress resource, including its name.

**spec**: The spec section of the Ingress resource is where you define the rules for routing incoming traffic.

**rules**: The rules field is an array that specifies one or more routing rules.

**host**: This field specifies the hostname to match for incoming requests.

**http**: Inside the http field, you can define rules for HTTP traffic.

**paths**: The paths field is an array that specifies how requests with specific paths should be handled.

**pathType**: Prefix: This line specifies the type of path matching to use, which is "Prefix." With Prefix matching, requests with paths that start with "/path" will match this rule.

**path**: "/path": This line defines the path prefix to match. In this case, it's set to "/path," so any request with a path that starts with "/path" will match this rule.

**backend**: The backend field specifies how traffic matching this rule should be forwarded to a Kubernetes Service.

**service**: This indicates that the traffic should be forwarded to a Service.

**name**: todo-app-nodeport: This specifies the name of the Kubernetes Service to which traffic should be routed. The Service named "todo-app-nodeport" will receive the traffic.

**port**: number: 8000: This line specifies the port number (8000) on which the Service should receive the traffic.

**Install an Ingress Controller.**

minikube addons enable ingress is used to enable the Ingress addon in a Minikube cluster.

**$minikube addons enable ingress** 

If you want to list all addons use command below

```
$minikube addons list
```
![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 032](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/0feeff9a-404e-45d3-ae5b-89e8ea0b9d80)


```
$kubectl get ingress
```
Now we can see that ingress configuration is synchronised. Before, the address field was not populated, but now it is. 

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 033](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/4c74a33b-c177-4f71-9aeb-3e5493db1844)


**To expose application to the internet**

```
$kubectl port-forward svc/todo-app-nodeport 8000:8000 --address 0.0.0.0
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 034](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/ab6d9af0-cf12-4b0d-85f9-e7bb4b3c01ba)


**kubectl port-forward**: This is the command for port forwarding in Kubernetes.

**svc/todo-app-nodeport**: This specifies the Kubernetes Service to which you want to forward traffic. In this case, it's the Service named "todo-app-nodeport."

**8000:8000**: This part of the command specifies the port mapping. It tells Kubernetes to forward traffic from port 8000 on your local machine to port 8000 on the Service. So, any traffic sent to localhost:8000 on your local machine will be forwarded to the specified Service.

**address 0.0.0.0**: This option allows you to specify the IP address on which the port forwarding should listen. Setting it to 0.0.0.0 means that the port forwarding will listen on all network interfaces, making the forwarded port accessible from any network interface on your local machine. If you omit this option or set it to the default, it will listen only on localhost (127.0.0.1)


**Access your todo-app**

Access the todo-app using **Ec2_ipaddress:8000**

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 035](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/473cb19b-c8df-4764-8664-72a0409fa543)


## ConfigMaps and Secrets

**ConfigMaps** are Kubernetes objects used for storing configuration data in key-value pairs. They are intended for non-sensitive data, such as environment variables, configuration files, or command-line arguments for containers. To use ConfigMaps, we can Inject ConfigMap data into pods as environment variables and can also Mount ConfigMap data as files in a container's file system.

**Secrets** are Kubernetes objects designed to store and manage sensitive information, such as passwords, API tokens, SSH keys, or certificates. Secrets are base64-encoded by default but can be mounted as files or used as environment variables in a similar way to ConfigMaps. To use Secrets, we can Inject Secret data as environment variables, Mount Secret data as files in a container's file system and Use Kubernetes service accounts to automatically mount Secrets in pods.

Best Practices:

1) Use ConfigMaps for non-sensitive configuration data.
1) Use Secrets for sensitive information.
1) Limit access to ConfigMaps and Secrets by using RBAC (Role-Based Access Control).
1) Avoid storing sensitive information directly in application code or Docker images.
1) Regularly rotate secrets and use tools like Kubernetes Secrets Store CSI Driver or external secret management systems for better security.

Create configmap.yaml

```
$vi configmap.yaml

$kubectl apply -f configmap.yaml
```
To Display a list of all ConfigMaps  

```
$kubectl get cm
```

To display detailed information about the ConfigMap

```
$kubectl describe cm test-configmap
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 036](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/6a51e081-c01a-4faf-aca4-ed72119e694d)


In deployment manifest include the ConfigMap

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 037](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/bd39cd62-76e8-46ff-bd37-5591f876d45d)


To see the key-value pairs of an environment variable in a ConfigMap inside a cluster or a pod

```
$kubectl exec -it <pod-name> -- /bin/bash
```
Then inside the pod search for environment variables that contain the string "DB." 

```
$env | grep DB
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 038](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/46ffc136-a4b0-4419-bece-2e719498f6c4)


Create a secret.yaml file

Then apply,

```
$kubectl apply -f secret.yaml
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 039](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/f8718e55-a580-41ff-9de7-6fcc0a7268fe)


In deployment manifest include secret.

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 040](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/f4b124cb-b394-46bc-8b7e-8f9f1ca0a61a)


Then apply, kubectl apply -f deployment.yml -n <namespace-name>

```
$kubectl apply -f todo_app_deploy.yaml
```

To verify that the Secret has been created
kubectl get secrets

```
$kubectl get secret
```

Display details of a specific Secret, kubectl describe secret <secret-name>

```
$kubectl describe secret dbpass-secret
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 041](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/92ed1bb5-6972-41d0-954f-295752d6401d)


We can see that db-pass is showing 11 bytes, which indicates that db-pass is encrypted.

## Volumes

Volumes are a way to manage and persist data in containers. They allow you to decouple your containerized application from the underlying storage infrastructure and provide mechanisms for sharing data between containers, pods, and even across nodes in a cluster. 

### Persistent Volume

Persistent Volume (PV) is a piece of storage in the cluster, which can be provisioned either dynamically or manually by an administrator. A Persistent Volume Claim (PVC) is a request for storage, and it can be made by both users and applications within the cluster. 


Create **persistence\_volume.yaml**

Create **persistent\_volumeclaim.yaml**

Then apply
```
$kubectl apply -f persistence_volume.yaml

$kubectl apply -f persistent_volumeclaim.yaml
```

To use the Persistent Volume Claim in your Deployment file, todo-app-pvc-deploy.yaml. You should add a volume and a volumeMount section to the container definition, which references the Persistent Volume Claim.

Then apply, 

```
$kubectl apply -f todo-app-pvc-deploy.yaml
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 042](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/a4c309bc-c624-4fb9-b05b-cb94d735ea00)


These commands will show the list of Pods and Persistent Volumes in your cluster.

```
$kubectl get pods

$kubectl get pv
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 043](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/fbc2819a-9ee4-4aaa-ba2c-3b3235944e07)


Connect to a Pod in your Deployment using 

```
$kubectl exec -it <pod_name> -- /bin/bash
```

Create file inside pod in app directory.

Delete the deployment and then again create deployment. 

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 044](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/9eae4648-cdb8-4ee2-b089-ba4c7b4b728b)


![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 046](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/8c3b8b54-3af2-4780-8319-0763e4cd3c94)


To access the data stored in the Persistent Volume from within the Pod go inside a pod and check the file which you have created.

In the above image we can see that file is showing in /app.

## Kubernetes Namespaces

Namespace is a logical and virtual cluster within a physical Kubernetes cluster. Namespaces provide a way to partition and isolate resources within the same cluster. They are used to organize and segregate objects such as Pods, Services, ConfigMaps, Secrets, and more. 

Lets understand in a simple way, think of a Namespace as a way to divide your big playground (Kubernetes cluster) into smaller sections. Imagine you have a sandbox, and you put different toys in different areas to keep them separate and avoid confusion.

In the same way, Kubernetes uses Namespaces to keep your computer programs and services separated from each other. Each program or service goes into its own "box" (Namespace), and they can't mess with each other or use the same names. It's like having different folders on your computer to keep your files organized.

Now lets create a Namespace for your Deployment.

```
$kubectl create namespace <namespace_name>
```

Now include namespace in deployment manifest. 

Then apply deployment,

```
$kubectl apply -f <deployment_name> -n <namespace_name>
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 047](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/84bfd5dc-e22b-4b03-8dad-03302e8760ab)


Check the Namespaces in your cluster.

```
$kubectl get namespace
```

Now to confirm that the namespace has been created or not.

```
$kubectl get deploy -n <namespace_name>
```

![Aspose Words cc492136-3d53-4fb8-b086-f64bbd7f8b4a 048](https://github.com/pradip2994/Kubernetes_k8/assets/124191442/42651b0e-728c-4f69-863d-b50af026bd56)


## RBAC ( Role Based Access Control )

RBAC is a crucial component of securing your Kubernetes cluster, helping you manage access control and reduce the risk of unauthorized or malicious actions within the cluster. It is a fundamental aspect of Kubernetes security and is essential for managing multi-tenant environments and complex containerized applications.

Depending on your role, you will define access. This is how you manage your user management. This is one part of RBAC. The second part is how you deal with service accounts. When you create a pod, you need to determine what access this pod should have to the Kubernetes cluster. Should the pod have access to ConfigMaps. Should the pod have access to secrets. Let's say a pod in your application needs to read a ConfigMap or secrets.

Now, suppose you have deployed a pod, and this pod turns out to be malicious. It attempts to delete data related to the API server. How can you restrict this access? Similar to user management, you can also control the access of your services or applications running on the cluster using RBAC.

RBAC has two primary responsibilities: user management and managing the services that run on the cluster.

On a broad level, there are three things in Kubernetes:

1) Service accounts/users
1) Roles/cluster roles
1) Role bindings/cluster role bindings. 

In linux we have user management to deal with users but Kubernetes does not deal with user management and offloads the user management to identity providers. In Kubernetes, the API server acts as an auth server.

RBAC Best Practices: 

When implementing RBAC in Kubernetes, it's important to follow best practices. This includes the principle of least privilege, which means granting the minimum necessary permissions to subjects. Regularly review and audit RBAC policies to ensure they align with your security requirements.




