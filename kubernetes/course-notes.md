
## Kubernetes Course Notes

These are my notes while watching the following course in Udemy:

https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/22776989#overview


What is K8s? 
- A system for running many different containers over multiple different machines.

Why use K8s?
- When you need to run many different containers with different images.

CLUSTER:
A cluster in the world of Kubernetes is the assembly of something called a master and one or more nodes.
We as developers communicate with the master node - which handles deployments in the other nodes. So we never actually manually log in into one of the containers in the secondary nodes. We communicate through kubectl API with the Master Node only.
	In essense we pass a 'list of responsibilities' to the master node and expect those to be fullfilled. While in progress the master node, constantly keeps checking this list and handles any restarts/changes to the other nodes . E.g. restarting a container running in a secondary node.

NODE:
A node is a virtual machine or a physical computer that's going to be used to run some number of different containers.


Development VS Production environments

- Locally we use MiniKube - a command line tool whose sole purpose is going to be to set up a tiny little Kubernetes
- Production: Managed solutions:
	+ Amazon EKS (Elastic Container Service)
	+ Google Cloud Kubernetes Engine (GKE)
	+ Azure AKS - Azure Kubernetes Service

MiniKube -> it's essentially going to create a virtual machine whose sole purpose is going to be to run some number of containers.
MiniKube is a program that is used to create this virtual machine or this single node on your computer. In order to interact with this thing, you and I are going to be using a program called KubeCTL.


#### client-pod.yaml
	apiVersion: v1
	kind: Pod
	metadata:
		name: client-pod
		labels:
			component: web
	spec:
		containers:
			- name: client
			  image: image/addr
			  ports:
			  	- containerPort: 3000


#### client-node-port.yaml
	apiVersion: v1
	kind: Service
	metadata:
		name: client-node-port
	spec:
		type: NodePort
		ports:
			- port: 3050 // for multi-client pod to communicate with this pod
			  targetPort: 3000 // identical to the containerPort
			  nodePort: 31515 // access container from browser 
		selector:
			component: web


#### client-deployment.yaml
	apiVersion: apps/v1
	kind: Deployment
	metadata:
		name: client-deployment
	spec:
		replicas: 1 // the number of different pods that will be created using the template below
		selector:
			matchLabels:
				component: web
		template:  // exact configuration to be used for pods inside the deployment
			metadata:
				labels:
					component: web
			spec:
				containers:
					- name: client
					  image: image/name
					  ports:
					  	- containerPort: 3000


apiVersion: each API version defines a different set of 'objects' we can use
kind - Object Type - e.g. Service, Pod, ReplicaController, StatefulSet

	Node - is a VM created by MiniKube - or a managed service if in a production environment
	Pod -  most basic object - created inside a Node - a grouping of containers with a similar purpose
	    - the smallest thing you can create in order to run an image/ container inside of it
		- has a primary container
		- has some support containers
		- multiple containers within a pod are interelated/interdependent
		- containers are specified in the spec section
	Service - sets up networking in a Kubernetes Cluster
		- has 4 subtypes:
			+ ClusterIP - exposes a set of pods to other objects in the cluster
			+ NodePort - exposes a container to the outside world (only for local development)
			+ LoadBalancer - legacy way of getting network traffic into a cluster
			+ Ingress - exposes a set of services to the outside world
	Deployment - maintains a set of identical pods, ensuring that they have the correct config and that the right number exists
		- Similar to Pods
		- Good for Production
		- we can change any piece of configuration tied to a pod that we want to
	Secret - securely stores a piece of information in the cluster, such as a database password
		- kubectl create secret <type_of_secret> <secret_name> --from-literal key=value
		- Types of secrets are: tls,docker-registry,generic

		label-selector - used a stategy for a service to identify another service (see component: web above)


Important Notes
 - Kubernetes is a system to deploy containerized apps
 - Nodes are individual machines (or vm's) that run containers
 - Masters are machines (or vm's) with a set of programs to manage nodes
 - Kubernetes didn't build our images - it got them from somewhere else
 - Kubernetes (the master) decided where to run each container - each node can run a dissimilar set of containers
 - To deploy something, we update the desired state of the master with a config file
 - The master works constantly to meet your desired state


### Imperative Deployments VS Declarative Deployments

 Imperative 
 	- Do exactly these steps to arrive at this container setup

 Declarative 
 	- Our container setup should look like this make it happen



Persistent Volume Claims
	-> Statically provisioned persistent volumes
	-> Dynamically provisioned persistent volumes



Access Modes (for PVS - Persistent Volume Storage)
	- ReadWriteOnce - Can be used by a single node
	- ReadOnlyMany - Multiple nodes can read from this
	- ReadWriteMany - Can be read and written to by many



### Helm

A package manager for K8s.

Helm is essentially a program that we can use to administer third party software inside of our Kubernetes cluster.
More info here: https://github.com/helm/helm

RBAC - Role Based Access Control
 + Limits who can access and modify objects in our cluster
 + User Accounts: Identifies a person administering our cluster
 + Service Accounts: Identifies a pod administering a cluster
 + Cluster Role Binding: Authorizes an account to do a certain set of actions across the entire cluster
 + Role Binding: Authorizes an account to do a certain set of actions in a single namespace

------------

### Shortcuts

	kubectl get pods 
	kubectl get services
	kubectl get deployments
	kubectl get storageclass --> see all the different options on your computer that Kubernetes has for creating a persistent volume.
	kubectl get pv --> get persistent volumes
	kubectl get pvc --> get persistent volume claims
	kubectl apply -f client-pod.yaml  -->> create or update object
	kubectl describe <object type> <object name> -->> get informatino about a particular object
	kubectl delete -f <config file> -->> pass the config file used to create this object (IMPERATIVE Command)
	kubectl delete service <service-name>
	kubectl delete deployment <deployment-name>
	kubectl set image <object-type>/<object-name> <container_name>=<new-image-to-use> -->> imperative commang to update image of object
	minikube ip -> in order to find what is the address of the pod you are running with minikube - NOT LOCALHOST

	eval $(minikube docker-env) --> sets up the current terminal window to work with minikube's VM docker


Flags:
 -o wide -->> get more details


TIPS:
 - Use all the same debugging techniques of docker with kubectl


### Terminology
- alpine: a term in the docker world for an image that is as small and compact as possible


