# Containers in the Cloud

## Kubernetes engine

- it’s like an IaaS - saves you infrastructures chores, lets you share compute resources with others by virtualizing the hardware
- PaaS - was built with the needs of developers in mind

### Containers

- a way to package software
- Containers start much faster than virtual machines and use fewer resources, because each container does not have its own instance of the operating system.

![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled.png)

- gives you independent scalability of workloads like you get in a PaaS environment and an abstraction layer of the operating system and hardware like you get in an IaaS environment
- the environment scales like PaaS but gives you nearly the same flexibility as IaaS. The container abstraction makes your code very portable
- You can treat the OS and hardware as a black box so you can move your code from deelopment to staging to production or from your laptop to the Cloud without changing or rebuilding anything
- The units of code running in these Containers can communicate with eac other over a network fabric. (this way you can make your applications Modular - they deploy it easily and scale independently across a group of hosts
- a tool that helps you do this well is Kubernetes.
    - it makes easy to orchestrate many containers on many hosts, scale them, roll out new versions of them and even roll back to the old versions if things go wrong
- The most common image of a container is the open source tool Docker
    - We gonna bundle an application and its dependencies into a Container, you could use a different tool for example Google Cloud offers Cloud Build
    - Lets say that you build python web application that uses Flask framework, whenever a web browser talks to it by asking for its top most document. oit replies “hello world”. Or if the browser instead append/ version to the request, the application replies with its version
        - How do we deploy this application? It needs a specific verwion of Python and a specific version of Flask which we control using Pythons requirements.txt file together with its othere dependencies too.
        - So you use a Docker file to specify how your code gets packaged into a Container.
        
        ![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%201.png)
        
        ![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%202.png)
        

## Kubernetes

- open source orchestrator for containers so you can better manage and scale your applications
- you control it through its API
- it lets you deploy containers on a set of nodes called a cluster
    - cluster is a set of master components that control the system as a whole and a set of nodes that run containers
    - A node represent a computing instance (In google cloud nodes are VM’s running in compute engine)
    
    ![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%203.png)
    
- to use Kubernetes we describe a set of applications and how they should interact with each other and Kubernetes figures out how to make that happen

### Kubernetes engine

![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%204.png)

- google lets you create your own cluster
- clusters can be customised and they support different machine types, number of nodes and network settings

### Pod

- whenever Kubernetes deploys a container or a set of related containers it does so inside an abstraction called a pod
- Pod is the smallest deployable unit in Kubernetes
- It can be one component of your application or even your entire application

![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%205.png)

- its common to have only one container per pod, but if you have containers with hard dependency you can package them into a single pod (they will share networking nad they can have disk storage volumes in common)
- each pod gets a unique IP address and set of ports for your containers
- containers inside a pod can communicate with each other using the [localhost](http://localhost) network interface, they dont care which nodes they are deployed on.

![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%206.png)

### Deployment

- represents a group of replicas of the same pod. It keeps your pods running even if a node on which some of them run on fails
- by default pods in deployment are only accessible inside your cluster, to make them available on the internet you can connect load balancer to it

### Service

- grous a set of pods together and provides a stable endpoint for them

if you need more power

- to scale a deployment run the kubectl scale command. Now our deployment has 3 nginx web servers but they re all behind the service and they are all available through one fixed IP address

### Configuration file

- you provide a configuration file that tells Kubernetes what you want your desired state to look like and Kubernetes figures out how to do it.

![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%207.png)

### Rolling update

- quick way to push out a new version of your application while still sparing your users from experiencing downtime

## Introducing hybrid and Multi cloud Computing

![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%208.png)

- move only some of your compute workloads to the cloud (it allows you to keep parts of your infrastructure on-premises while moving other parts to the Cloud)
- move at your own pace
- take advantage of clouds scalability and lower costs

### Anthos

- google’s modern solution for hybrid and multi-cloud systems and services management
- framework

![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%209.png)

- Enterprise applications may use hundreds of microservices to handle computing workloads. Keeping track of all of these services and monitoring their health can quickly become a challenge. Anthos, an Istio Open Source service mesh take all of these guesswork out of managing and securing your microservices.
- These service mesh layers communicate across the hybrid network using Cloud Interconnect to sync and pass their data

### Stackdriver

- offers fully managed logging, metrics collection, monitoring dashboarding and alerting solution that watches all sides of your hybrid and multi cloud network

![Untitled](Containers%20in%20the%20Cloud%20edab3c4d453c4fc198b1b5684fe2beef/Untitled%2010.png)