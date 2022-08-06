# Kubernetes deep dive

## Intro

Open source platform for running cloud native apps

You have some infrastructure on a cloud platform, but you need something on top of it to run your apps on. That is kubernetes, it provides a rich API for running cloud native apps

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled.png)

**Cloud native app**

cloud-native apps are a collection of small, specialized components, usually containers that come together to form a meaningful application.

- easy to scale and update

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%201.png)

Kubernetes is a platform of choice when it comes to running these cloud native apps (it provides API for anything that you need like scaling)

## What components does it have

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%202.png)

Kubernetes cluster is made up of a bunch of Linux nodes,
VMs or cloud instances. But some of them form the control plane,
and others, the worker nodes. The control plane's the brains
of the cluster where all the magic happens. Workers, I think the name speaks for itself, this is where your apps run.

API is the gateway to the cluster, the API server is the grand station of the control plane (all requests to get, update, list, delete things from the cluster go through the API server) - so as an admin you are talking only to the API server when you are deploying or managing your apps, BUT also all the nodes and the bits of the control plane are talking to the API server as well.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%203.png)

You have your cluster, and you post requests to the API server to deploy and manage apps. The scheduler and the controllers take care of the mechanics of making those requests happen,
and your apps actually run on the worker nodes.

**Summary**

So real quick, you write your code in a cloud-native way,
lots of small specialized microservices. These all talk to each other over their own APIs. You package them up in a way that will run on Kubernetes, and you feed them to the API server, and Kubernetes takes care of running them.

## Kubernetes API

- place where everything in Kubernetes is **defined**

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%204.png)

- everything is a resource defined in the API
- a RESTful API, that uses standard HTTP methods are verbs
to perform CRUDE style operations
- for the most part, our interaction with the API, is gonna be through the `kubectl` command line utility.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%205.png)

We'll define the different parts of our apps in YAML files.
And we'll use kubectl to post them to the API server, assuming we can authenticate, that'll create a record of intent on the cluster in the store. Record of intent changes the overall desired state of the cluster which in turn, causes the other bits of the control plane
to kick into action.

### Declarative configuration

the Kubernetes way of deploying and managing apps,
is to define the various parts of those apps in YAML file,
you post these to the API server is a record of intent,
and this updates the overall desired state of the cluster.

- in the background,the control planes running a ton of watch loops that are constantly checking, that the current observed state of the cluster, matches the current desired state.
While posting a new YAML file, that changes the desired state.
So before long, the watch loops will notice, and various parts of the control plane kick into life, to bring that observed state
into line with the new desired state. I don't know an example might be a cluster with let's say, five running replicas of a service that compresses images. If you post an updated YAML file to the cluster, changing the desired state to be 10 replicas
instead of five. Well, the current observed state is gonna be out of sync, with this new desired state, watch loops will notice,
and controllers will kick into reconcile. And it's a beautiful thing.
I mean, those YAML files are your source of truth.
And they serve as get this living application documentation.
Sounds cheesy, right? But it is the absolute business.
We all want decent documentation. And this type of declarative model, it gives it to us for free, I love it. You basically define your app and YAML files, that are great documentation, then you give those to the cluster and it deploys your apps. NET NET, your documentation is always up to date.

### API groups

- there is a lot of API groups

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%206.png)

- so for example all the  workload stuff, like deployments, and replica sets and demon sets, and the likes, these are all in the apps API group.
- Lots of groups, each with their own resources
- Each of these API groups is kind of looked after by a special interest group a SIG (it is actually a group of real people that are responsible for feature development)
- Each API group is versioned

```jsx
kubectl get apiservices
```

## Kubernetes objectives

A major force driving cloud native is containers.
I mean there's serverless and other stuff as well right,
but containers are the poster child for cloud native.
Only shock horror, Kubernetes doesn't run containers
or at least it doesn't run them directly.
It wraps them in a high level construct called a pod.

- so the smallest thing you can deploy on a kubernetes cluster is a pod, but inside of each pod is one or more containers (where application code exists)
- pod is an object on the cluster and its defined in the API as a resource in the core API group
- But pods on their own don't give us a great deal.
So we wrap them in a high level object called a deployment.
This again, is an object on the cluster and it's a resource in the apps API group.
- The whole idea of deployment is to make pods scallable (making rolling updates and rollback simple)
- So, pods and deployments exist in the API. They can be deployed on the cluster as objects and they're two of the key primitives
that make Kubernetes an ideal platform for cloud native micro services apps.
- Now, deployments are great for scaling and updates
but other objects exist for wrapping your pods. So, DaemonSets make sure that one and only one of a specific pod will run on every worker in the cluster. And then we've got stateful sets for pods or parts of your application with particular stateful requirements.

### Stateful vs stateless

Stateful services keep track of sessions or transactions and react differently to the same inputs based on that history. Stateless services rely on clients to maintain sessions and center around operations that manipulate resources, rather than the state.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%207.png)

## Ways to spin up a cluster

- Play with kubernetes (4hour lab) (https://play-with-k8s.com)
- Local kubernetes with Docker
- For hosted options - you can use microsoft, AWS or Google

## Kubernetes App theory

These could be the requirements and then we start coding

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%208.png)

- Microservices are fore xample the external facing web service and Persistent back end
- At some point we will get to a frontend that communicates with the backend, but how do we then do this in a cloud native way?
    - well first we obviously need a cluster
    - lets say that we are running the services (frontend, backend) as containers (that's not to say that you can't use serverless or VMs if you think they're better suited. But you get the picture)
    - You have a kubernetes cluster, then you take your code and your front-end web service and you build it as a docker image. Same goes for the back-end database. And you end up with two container images.
    - Then for the load balancer here, Kubernetes has this Service object, capital S Service, and it's a resource in the API.
    And if you're running on a cloud platform, you can build one of these that actually spins up an internet-facing load balancer on your cloud. Well, bingo. That's the load balancer sorted.
    - Now you're accepting requests, and you wanna balance them across the web tier here, which over time you expect to scale up and down as demand ebbs and flows. So you wrap your web containers in a Kubernetes construct called a Deployment. (actually, you know what? Containers get wrapped in pods, and it's actually the pods that get wrapped in the Deployment)
    - Then we add in some secrets to get them all talking to each other.
    - But to tick off the persistent storage requirement,
    we throw in a persistent volume and a persistent volume claim. (resources in the API)

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%209.png)

so basically all is defined as an object in kubernetes

## Kubernetes sample app

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2010.png)

- so you defined the objects in a yaml file that you then give to the API server with the kubectl command and let the Kubernetes do the rest. The frontend and backend are just two containers that have the necessary code.

## Recap

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2011.png)

You have some project idea → make the requirements → start coding → build container images → map each of the components (load balancer, web frontend , DB backend) into kubernetes objects (write it all in a declarative yaml file)

## Networking

In a modern app, every piece of logic seems to be its own microservice these days. And each one of those microservices
is a discrete network end point. So it has its own IP address
and of course they're all talking to each other like all of the time.
So, if you've got a crappy network, you're gonna have a crappy app and that's just bad for business.

### OLD DAYS

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2012.png)

### NOW

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2013.png)

instead putting everything together, we split it out, and code it seperately.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2014.png)

Well, on the network in front, all of these services here are end points. So they all need IPs, and they all need to know how to find each other. So we need a solid and a dynamic DNS, right?
I mean these end points are coming and going like mad.

**CHURN -** endpoints being added and removed from the network

Highly dynamic networks (scalable) are the new normal

Example

### Demo

we put bunch of pods running containers with wordpress on port 80

then we front it with a service, this time a cloud native load balancer that gives a way to our application from the internet

## Kubernetes networking

Rules:

- all nodes in the cluster have to be able to talk to each other
- all pods on the network can communicate with each other without NAT
- every pod gets its very own IP address

First off, we've got two networks, node and pod. Now, Kubernetes itself doesn't implement the node network. But like we said, all nodes need to talk, and it's basically
these pods here, though, you might need more depending on what solution you chose for the pod network. Speaking of which, Kubernetes does implement
the pod network, or it kinda does, right? I mean, it presents a network plugin interface called the CNI, Container Network Interface. And then third parties actually provide the plugins that implement the pod network

- The pod network is big and flat. Normally an overlay of sorts, right?
So it's stretched across all nodes and every pod has an IP on it.
- General idea is yes, it's big and flat and each node gets allocated a sub set of addresses from it. Then, as pods are spun up, they get scheduled to a particular node. The IP address that they get is one from the range of addresses allocated to that node. But the cool thing, this IP here that the pod gets is not only visible and reachable from all nodes and all pods, it is also the address that the pod sees itself as. So there is no network voodoo going on here, where you've got one address on the inside of the pod, but then another one on the outside on the network. Nah uh, the pod sees itself as this address and so does everything else on the network.
So think of it like this, right? It's a networking party and every pod is invited. And once you're in, there's no VIP lounge or tiered system where only certain endpoints
are reachable, yeah? Well, at least not out of the box there's not. I mean, you might be able to add that later. But out of the box, right, the Kubernetes pod network
is an open invite party. And once you're in, you are free to talk with whoever the heck you like. And at the highest level, that is the very basics of Kubernetes networking.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2015.png)

## Kubernetes services

Instead of trying to hit individual Pods down here that can come and go, hit the Service instead." And obviously, the Service's clever enough to handle all the churn

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2016.png)

- every service gets a name and an IP (they are **stable -** will never change for its entire life)

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2017.png)

- The name and IP gets registered with the cluster's built-in DNS, or add-on DNS, yeah? So every Kubernetes cluster has a native DNS Service.I mean, you might have to manually start it, OK,but every cluster can have a native DNS Service,
and every Pod in a cluster knows how to use it. So in the example on screen, right?
It means every single Pod in our cluster can resolve search API here and reach this Service.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2018.png)

Think of Services here as load balances or proxies. They've got a frontend config and also a backend one. Well on the backend, it needs to know which Pods
to send the traffic onto, yeah? Well, we could do that with a label selector.
Now, this here example's saying, "OK, "balance traffic across all Pods in the cluster
"with this label here," and you know what? We can list multiple labels and what have you, right? But this is the basic config. This is the name in the IP on the front,
and maybe a port as well. Hit me on this. And when you do, I'll balance your traffic
across all of the Pods in the cluster with this label... But how does the Service actually know which Pods are alive and kicking?

You see, when you create a Service object with a label selector,
Kubernetes also creates another object on the cluster called an "endpoint object,"
and what that is is a list of Pod IPs and ports that match the Service's label selector.
So, in our example, the endpoint object for the Service will have three entries,
one for each of the three Pods, yeah? But the cool thing? The Service object is always watching the API server to see if new Pods that match its selector are being added or removed, and as they are, it automatically updates the list in the endpoint object.
Right, so the endpoint object itself always has the same name as the Surface object it's associated with, and it is a list of Pods that the Service can send requests to.

So, a client makes a request into this frontend config of the Service,
and then for the Service to know how to forward requests on, instead of doing some on the fly lookup to see which Pods on the cluster actually currently match the label selector, it just picks one from the endpoint list 'cause it's always up-to-date.

## Service types

- 3 different ones
    - LoadBalancer
    - NodePort
        - Gets cluster-wide port
        - Also accessible from outside of cluster
        
        ![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2019.png)
        
        So to reach a particular service (node) you just take its IP and append it with the NodePort
        
    - ClusterIP
        - default and most basic (thats what you get when you dont specify other)
        - Gets own IP, only accessible from within cluster
    
    ![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2020.png)
    
- they provide a stable abstraction point for a bunch of pods

## The service network

When you create you create your service it gets this, unique, long lived IP. Cool, we know that. But I don't know if you noticed, that IP's actually not on any network that you recognize. So it's not on the Node Network, and its not on the Pod Network.
It's actually on this third network that we call the Service Network.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2021.png)

**But its not really a network, so how does it even gets traffic?**

- Every node on the network has this process running called kube-proxy.
Actually, it's running on the cluster as a DaemonSet. So you get one kube-proxy pod on every node. Anyway, one of it's main jobs is to write a bunch of IPVS, or
IPTables rules on each node, that basically say, any requests that you see addressed to this service network, rewrite the headers and send them to the appropriate pods on the pod network.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2022.png)

## Kubernetes Storage

First up, the basic premise of volumes in Kubernetes is to abstract storage or data from pods. So, without volumes, your data lives and dies with the pod it's associated with. You spin up a pod, write some important data to it, the pod crashes, or gets scaled out, or whatever, and it's goodbye data.

- With volumes, though, we get to create and manage volumes as volumes, so they exist on the cluster, in their own right. Then, if a pod wants to use one, it needs to lay a claim to it, and mount it. Then if the pod dies or whatever, the volume still exists. It is absolutely not tied to the life cycle of the pod.

Requirements

- Speed?
- Replicated?
- Resiliency?
- Do all pods need to be writable?

Kubernetes leaves all of that stuff to the **storage provider**

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2023.png)

- you have the storage on the left, then you have the CSI (container storage interface) to communicate with the kubernetes cluster and on the right side you have the Kubernetes persistent volume subsystem

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2024.png)

## Container Storage Interface (CSI)

Using CSI, third-party storage providers can write and deploy plugins exposing new storage systems in Kubernetes without ever having to touch the core Kubernetes code.

## Kubernetes Persistent Volume Subsystem

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2025.png)

On the right we have a storage from your cloud provider, this hooks into Kjubernetes via CSI plugins then on the Kubernetes side we have volumes called PersistentVolumes (PVs) which has attribute like size

It is a bunch of storage taken from a storage backend and made available inside the Kubernetes cluster. And it's all decoupled from pods, remember.

So we create the PV on the cluster, and it exists independently, just like a pod or a node. Well, to use it, a pod needs a PV claim, a PVC. And again, like a node or a pod or a PV, yeah, a PVC is a resource in the API, and an object on the cluster.

### Access modes

- RWO: ReadWriteOnce
    - can only be mounted as a readwrite by one Pod in the cluster
- RWM: ReadWriteMany
    - can be mounted and readwrite by many pods in the clusters
- ROM: ReadOnlyMany
    - can only be read by many pods

### Reclaim policy

What the cluster does when a claim on a volume is released

- Delete
    - release a claim on a volume and Kubernetes will delete it (and also will delete it on the storage backend)
- Retain
    - keeps the volume and its contents
    - So you can release a claim, or, you know what,
    even delete or fail the pod that's using it,
    and the volume, including its data, that sticks around.
    Separate life cycles, yeah?

PVC = Persistent Volume Claim is also just a resource (object in the cluster) that you create with a yaml file

### Recap

You start with your storage, an array or a cloud service. That plugs into Kubernetes. I'm on Google Kubernetes engine, but it works the same in AWS and Azure, or whatever you have.
Then you create some devices or shares on that backend. And then it's a case of creating a PV that matches it. And it's the PV that makes the backend storage actually a thing on the cluster. Then to use it, you create a claim that matches its attributes.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2026.png)

## Dynamic provisioning with Storage Classes

Storage needs to be dynamic. Like, there's no way a cluster admin or whatever can be manually provisioning volumes for pods, it just doesn't scale. Well, enter StorageClasses and dynamic provisioning,

- StorageClasses enable dynamic provisioning of volumes.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2027.png)

Anyway, we create one or more storage classes, and you can have as many as you want, right?
But each one relates to a particular storage back end by referencing a plugin. The official term for a plugin in the YAML files is provisioner, and we'll see it in a second.
So, as an example right, if you've got a Portworx and maybe a StorageOS on the back end, each one's gonna have its own plugin, or provisioner, and each of your storage classes that you write, is gonna reference one of those. All right, well, like everything else, a storage class is an API resource, so it's defined in a YAML file. And in there, as well as referencing the provisioner, you give it a bunch of parameters. Now, some of them you'll already know, like access mode and reclaim policy, but you also give it values that relate to stuff on the backend itself.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2028.png)

Now, if we list it, it should show as bound, so already bound to a PV, and all without us manually creating a PV, 'cause remember, we've created the fast storage class, and we've plugged it in to the AWS elastic store back end. Then, our storage class says, hey, any time a new PV claim comes along asking for storage from me, go ahead and dynamically create it on the back end,
and, create the PV on the cluster.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2029.png)

it is implemented through a control loop So the persistent value subsystem has a control loop constantly running and watching the API server for new PVC objects, and any time it sees one, it actions it.

## Getting code into Kubernetes

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2030.png)

You write your code, then you bundle it up with all of its dependencies into a Docker image. Then you put that in a registry and you know what up to this point, it's fair to say these steps are not really kubernetes but they absolutely need doing for to be able kubernetes to run your up anyway. Then we create a Kubernetes object that references the image we just made
and includes a bit of stuff. Maybe that tells kubernetes how to run it.

When I say kubernetes object, there's a few options. We could wrap the container in a pod and that works okay, but we never do it right. We tend to wrap everything in a high level construct
like a deployment or maybe a demon set or a StatefulSet.

**Workflow**

You lump your code and its dependencies into a directory and then you write a Docker file telling Docker how to build it all into an image. In case this is all new to you, You've got your code and stuff in a directory. Then you throw in a Docker file. That's basically a list of instructions on how to take that code and make it into a Docker image. We'll see it all in the sack. Then we run Docker build, we tell it what to name the image and where the Dockerfile is and we said back while Docker does its magic and after however long it takes out pops a Docker image. Then you take that image on your, push it to a registry, which absolutely can be on prem or in your private cloud.
Now, in our examples, we'll be using Docker hub on the internet. In the real world, you're going to be pushing to your own registry on prem or in your private cloud. Well, then after all of that comes the kubernetes stuff. Here was showing a deployment manifest file that basically says, we're not showing it all here, because if we did, it'd be so small you'd need like superhero vision, but I think we can say the basics. We're taking the Docker image from the previous stage. Let's roll that out as a Kubernetes deployment please, and we'll have three replicas, like I said,
there's a bunch more to it and we'll see it soon enough, but that's the flow.

## Kubernetes Deployments

Deployments are higher level object than pods.
In fact, the same way that pods wrap containers
we could say that deployment wraps pods.

- they are all about scaling and updates
- actually behind the scenes there's also something called a replica set-in play. So, the replica sets sits in between the deployment and the pod and then it's the replica set that actually takes care of any of the mechanics of scaling-related operations that the deployment kicks off.

## Scaling applications

### Horizontal pod autosclaler

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2031.png)

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2032.png)

Load increases on your app. And like we said, different apps are sensitive to different types of load. For one app, it might be CPU cycles, For another, it might be open connections.
But generally speaking, dealing with increased load means adding more pod replicas. That's where the Horizontal Pod Autoscaler kicks in. It increases the replica count in a deployment object. Well, this updates the desired state on the cluster, watch loops in the control plane, notice the change. And a replica set roles of it's slaves, and we get more pods.
So far, so good. But if the cluster is full, and there aren't any nodes with enough capacity to take these new pods, then those pods are gonna go into the pending state. Mm-hmm, not looking so good now, are we? No sweat though. Pretty soon, every 10 seconds I think, the Cluster Autoscaler is gonna check the pending pods. When it finds some, it's gonna add some nodes to the cluster. Once they spin up, those pending pods can be scheduled. And obviously the hope is, that the increased load is taken care of.

- Okay, if we attach it to this deployment and then we throw some work at it, and it uses more than 10% of a CPU, a hundred millicores, or whatever, that's going to breach this rule here that's saying, keep it below 50% of what we've asked for and it'll trigger a new pod. So a pod asking for 20% of a CPU, an HPA object keeping an eye it by waking up every 30 seconds by default and checking it's not using
more than 10% of the CPU. If it is, spin up a new pod. Good stuff.

### Cluster autoscaler

- all about right sizing your cluster for your apps
- you enable it on a cluster, and you configure pools of like nodes, just groups of identically spec'd nodes, yeah. So, like an autoscaling group or something, but provided by your cloud's hosted Kubernetes service. And that's important. It's not just any old scaling group on your cloud. These are tied into your cloud's Kubernetes service, and you can have a bunch of them if you need, like if you need different size nodes and the likes. But you have a node pool and you give each 1 a maximum and a minimum value.
Maximum's the most nodes it can have and minimum's the least.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2033.png)

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2034.png)

- Now then, let me reiterate. This putting pods into pending and the subsequent spinning up of new nodes and the likes, is all based on what pods are requesting, not what they're actually using. So the cluster can be practically idle. But if you are running pods that have asked for resources, that's what gets taken into consideration.

Okay, so the cluster autoscaler wakes up every 10 seconds.
That's when it checks with pending pods. Obviously, it can grow and shrink your cluster, but it's got a few checks and balances built in, so that it's not overreacting to like every twitch in the cluster. For example, one of those is wait 10 minutes before removing a node. So even if a node might be idle and there might be space elsewhere in the cluster for its pods, before going ahead and turning it off, the cluster is just going to watch it for 10 minutes first, just in case circumstances changed. Well obviously, it works alongside the horizontal pod autoscaler. I think I already said that
but as HPAs add pods, if any of them go pending due to insufficient node resources, the cluster autoscaler kicks in and grows the cluster.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2035.png)

## RBAC and Admission Control (security)

Anyway, the client talks to the API server,and it's HTTPS, yeah? Now, the certificates and stuff are all done by the installer, so if you're on a hosted Kubernetes on a cloud provider, or if you're installing it yourself, right? It doesn't matter, certificates are taken care of. I mean, you can obviously use your own CA if you want, but out of the box, you're getting, at the very least, a set of self-signed certs.
Anyway, once all the TLS is established, the authentication phase kicks in. Now, sometimes we call this authN, yeah?
Well, this phase is all about looking at the request and saying, right, this request to do whatever, maybe spin up a new deployment, well, it's been requested by the user Nigel. Well, how do we make sure it actually is Nigel? Detail obviously to come, yeah? But it does its magic and it verifies that, yes, this is Nigel, or no, it's an impostor. Well, after authentication, it's authorization, and this is the RBAC bit, right? That bit that says, "Okay, now that we know this. Is Nigel actually allowed to perform this action?" Create the deployment or whatever, yeah? Again, details to come, but the authorizer runs a bunch of checks, and either allows or denies the request. And that's really the RBAC stuff done. But it is not the end of the API admission process. Next up is this thing called Admission control. So, once the authN and the authZ stuff is done, we can configure admission controllers to modify and validate requests. So, on the modification, or mutation front, you might implement a policy that forces all parts goin' into particular namespace to get a certain label. Or maybe you wanna force all images to come from a particular repository, right? Well, all that kind of stuff, is the job of a mutating admission controller. After they're done, validation controllers kick in. And as the name suggests, they validate objects or requests. Cool, well after that, we get a bit of object specific validation as well. But if the request passes through all of these gates? Then we're in business, it's persisted to etcd, and it's instantiated on the cluster.

### Authentication

It's all about proving you are who you say you are. 

Requests come in to the API server with creds attached,
they get checked and the authentication module says either,
"Yep, authorized user, or no dirty imposter."

**3 options:**

- bearer tokens
- client certificates
- bootstrap tokens

You cannot create users in Kubernetes. So if you wanna lock things down with users and groups, which I promise you do,
you're gonna have to manage those outside of the cluster. But it can totally be active directory or your clouds, IAM provider or it can just be a list of Bearer tokens or maybe client certs.

A really simple example is client certificates. Every cluster I've ever worked on gets to CA. You can use that CA to mint user certificates. you embed usernames in the CN property of the certificate, and any groups get listed as organizations or the O property. Then you create a queue CTL context so that your certificate gets embedded with all future commands. Then when you post your requests to the API server, it checks your embedded cert against the CA and says, "Yep, that's one of ours or no, not created here." And that's it, now, that's a simple example.

![Untitled](Kubernetes%20deep%20dive%209341ee983c244fd996e6e156eb911953/Untitled%2036.png)

Now then, what we've been talking about here, are regular users for humans like us, to use with our kubectl commands,
but there's another type of user called a service account. And those are stored in Kubernetes. Only, they're not for you and me to use. They are for system components like kubelets, and the different parts of the control plane, 'cause remember, they need to authenticate with the API server as well. So for the most part, right, service accounts are created and managed by the cluster. Most of them live in the cube system namespace, and their credentials are stored in secrets. Great, but from a strategic security perspective, you need to give some thought,
as to how you wanna manage these. So like, do you want every object in the namespace, to have its own service account Okay, maybe you do, but probably not. I don't know, it seems a bit overkill. Maybe one per deployment or something might be a good idea. As usual, though, it's a trade off with like, granular generally being, the better, but harder to manage. So it's your call, choose what's best for your environment. The point is, every pod and every member of the control plane that interacts with the API server, gets associated with a service account. And that service account is the identity that you use,
when authenticating with the API server, fabuloso.

### Authorization

Well, this is where we really meet RBAC.

So, the architecture of the model is like this:
which users can perform which actions, on which resources?
That's RBAC.

when you create a new cluster, you get a context, and a user that has got mega-permissions. And that's all good, right,
for labs, and the likes? But, it is the opposite of what you need for production. So, you need to create users, and start opening things up. So, taking an RBAC-enabled cluster and a new user.
Nigel, or whatever, yeah? We need to create two objects to grant permissions. Roles, and RoleBindings.

### Admission control

Admission control kicks in after we requested the API server
has been both authenticated and authorized.
And the name of the game for it is to make sure that
policies and standards are in force.

- I don't know maybe you want all pods in a certain cluster
or a name space to get certain labels, yeah.
Or maybe you want to force images to
always be pulled from a registry.
Or even from a particular registry right?

Anyways, there's effectivity two main types
of admission controllers. **Mutating** and **validating**.
Look there names make it easy yeah? Mutating ones let you modify requests and the validating ones don't. They kick in here so its slightly different stages in the chain but right near the end right after all of the auth stuff. Now then, you can totally have multiple mutating and validating controllers in effect. And if you do, be aware of this right. They have all got to allow the request. So if just a single one of them says no,
that puts an end to the request.