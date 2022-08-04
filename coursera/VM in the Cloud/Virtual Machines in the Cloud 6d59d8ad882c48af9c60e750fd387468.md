# Virtual Machines in the Cloud

## Virtual Private Cloud (VPC) Network

- the way you can start with GCP is to define your own Virtual Private Cloud inside the first GCP project (or simply choose the default VPC)
- connects your GCP platform resources to each other and to the internet
    - you can:
        - segment your networks
        - use firewall rules
        - create static routes to forward traffic
- have global scope
    - you can have resources in different zones on the same subnet
- In this example the VPC has one network, so far it as one subnet defined in GCP as us-east1 region, it also has two compute engine VMs attached to it, they are neighbours on the same subnet even though they are in different zones

![Untitled](Virtual%20Machines%20in%20the%20Cloud%206d59d8ad882c48af9c60e750fd387468/Untitled.png)

## Compute engine

- lets you create and run VMs on google infrastructure
- you can run thousands of Virtual CPUs on a system that is designed to be fast and to offer consistent performance
- no upfront investments
- create by using GCP console or gcloud
- can run linux or windows server images
- when you create a VM:
    - pick memory and CPU
    - pick GPU if you need them
    - pick persistent disks (standard or SSD)
    - pick a boot image (Linux or Windows server)
    - you can pass a startup script that defines the configuration
- once VMs are running you can take durable snapshots as backups of the data
- Preemptible VM
    - you give it permission to terminate itself if its resources are needed elsewhere

![Untitled](Virtual%20Machines%20in%20the%20Cloud%206d59d8ad882c48af9c60e750fd387468/Untitled%201.png)

## Important VPC capabilities

- much like physical networks, VPCs have routing tables, they are used to forward traffic from one instance to another instance within the same network (even between sub-networks and even between GCP zones without requiring an external IP address)
- you can control to restrict access to instances, both incoming and outgoing
- For example, you can tag all your web servers with say, "web," and write a firewall rule saying that traffic on ports 80 or 443 is allowed into all VMs with the "web" tag, no matter what their IP address happens to be.

### VPC peering

- establish a peering relationship between two VPCs so that they can exchange traffic
- use to interconnect networks in GCP projects

### Shared VPC

- when you want to use the full power of IAM to control who and what in one project can interact with
- use to share a network or individual subnets with other GCP projects

### Cloud load balancing

- fully distributed software defined managed service for all your traffic
- you can put your Cloud load balancing in front of all your traffic - HTTP and HTTPS other TCP and SSL traffic and UDP traffic
- a single anycast IP frontends all your backend instances in regions around the world. It provides cross region load balancing
- reacts quickly to changes in users, traffic, backend health, network conditions and other related conditions.
- HTTPS load balancer, SSL proxy load balancer, TCP proxy balancer
    - intended for traffic coming into the google network from the internet

- Internal load balancer
    - if you want to load balance traffic inside your project
    - load balance across compute engine VMs

![Untitled](Virtual%20Machines%20in%20the%20Cloud%206d59d8ad882c48af9c60e750fd387468/Untitled%202.png)

### CLOUD DNS

- DNS is what translates internet host names to addresses
- creates managed zones, then add, edit delete DNS records
- Programatically manage zones and records using RESTful API or command line interface
- low latency and high availability
- Google cloud CDN - accelerate content delivery in your application
    - my customers will experience lower network latency

Once you setup HTTPS load balancing, simply enable cloud CDN with a single checkbox

![Untitled](Virtual%20Machines%20in%20the%20Cloud%206d59d8ad882c48af9c60e750fd387468/Untitled%203.png)