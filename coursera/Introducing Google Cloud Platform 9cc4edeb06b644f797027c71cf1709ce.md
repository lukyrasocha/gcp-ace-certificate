# Introducing Google Cloud Platform

# Learning objectives

- Explain the advantages of Google Cloud Platform.
- Define the components of Google's network infrastructure, including: Points of presence, data centers, regions, and zones.
- Compare Infrastructure-as-a-Service (IaaS) and Platform-as-a-Service (PaaS).

## GCP services

- compute
- storage
- big data
- machine learning
- Google Cloud Platform lets you choose from computing, storage, big data, machine learning and application services for your web, mobile, analytics and back-end solutions. It's global, it's cost effective, it's open source friendly and it's designed for security.

![Untitled](Introducing%20Google%20Cloud%20Platform%209cc4edeb06b644f797027c71cf1709ce/Untitled.png)

## Cloud computing

- way of using IT that has
    - On-demand self service (No human intervention needed to get resources)
        - you can get all the services without having to talk to people
    - Broad network access (Access from anywhere)
        - you can ask for the services from anywhere
    - Resource pooling (Provider shares resources to customers)
    - Rapid elasticity (get more resources quickly as needed)
        - you can get as many services you need, or reduce it
    - Measured service (pay only for what you consume)
    

### Why

- For efficiency
- It is virtualization (instead of having physical disks, we use the cloud)
- container based architecture - third wave cloud built from automated services
- Every company is a data company - google cloud provides services to manage data

### Infrastructure as a Service (IaaS)

- provide raw compute, storage and network organized in ways similar from data centers
- step away from on-premises infrastructure (services like storage and virtualization via cloud through the internet)
- As the user you are still responsible for OS any data, applications, middleware and runtimes but the provider (google) gives you access to and management of the network, services, virtualization and storage
- you don’t maintain your own on-site datacentre, you access and control the infrastructure via API
- Pay for what you allocate

### Platform as a Service (PaaS)

- Bind application code you write to libraries that give access to the infrastructure your application needs
- Provider hosts the hardware and software on its own infrastructure and delivers this platform to the user as an integrated solution through an internet connection
- You write the code, build and manage your apps, but you do it without the headaches of software updates or hardware maintenance - the environment to build and deploy is provided for you
- Pay for what you use

Before cloud computing you had to buy everything before hand (risky)

On-premise IT infrastructure presents the biggest level of responsibility to you as a user and manager. When your hardware and software are all on-premises, it’s up to you and your team to manage, update, and replace each component as needed. What cloud computing allows for is the allocation of one, several, or all of the parts of your infrastructure to the management of a third party, freeing you up to focus on other things.

### Software as a Service (SaaS)

- gmail, docs, drive

![Untitled](Introducing%20Google%20Cloud%20Platform%209cc4edeb06b644f797027c71cf1709ce/Untitled%201.png)

![Untitled](Introducing%20Google%20Cloud%20Platform%209cc4edeb06b644f797027c71cf1709ce/Untitled%202.png)

GCP is organized into regions and zones

## Zones

- deployment area for GCP resources
- picture it as a physical building
- you usually spread the resources across multiple zones in a region (brings applications closer to users around the world and also protects against the loss of an entire region)

## Regions

- zones are grouped into regions
- independent geographic areas (you choose which regions your GCP resources are in)
- All the zones within a region have fast network connectivity among them

![Untitled](Introducing%20Google%20Cloud%20Platform%209cc4edeb06b644f797027c71cf1709ce/Untitled%203.png)

## Environmental responsibility

- 100 % carbon neutral
- renewable energy
- ISO 14001 certification

## Open APIs

- you don’t have to be stuck with GCP,
- GCP services are compatible with open source products (Hadoop, Tensorflow)

## Multi-layer security approach

- How does google keep customers’ data safe?
    - hardware security chip Titan
    - Google server machines use cryptographic signatures to make sure they are booting the correct software
    - Access to to physical data centres is limited to only a very small fraction of Google employees
    - Encryption of hardware (hard drives and SSD)