# Chapter 3

# Context

Competition

- AWS (leader in this space)

Google innovation

- all about big data
- MapReduce, google File System, Colossus
- Kubernetes
- Big Table, Spanner, GCS,BigQuery

Google compared to AWS is more developer based

- they really expect you to have some developer knowledge

## GCP Structure and Design

### Design principles

- Global
- Secure
- Huge Scale
- For developers

GCP is intrinsically global

- Easier to handle latency and failures in a global way

### Physical infrastructure

- vCPU
- Physical server
- Rack
- Data center (building)
    - Few data centers are logically grouped together into a zone
    - each zone is as independent from other zones as possible
    - zones are grouped together into **REGIONS**
    - regions are grouped together into **MULTI-REGIONS**
    - All of there regions, zones etc are connected via Private global network (so communication from one server to another does not even have to touch the internet)
        - Points of Presence (POPs) - network edges where google actually connects to the internet
    - ALL OF THIS together creates the global system

![Untitled](Chapter%203%2085f44d5952f74cbbb2db5b877e32ba0d/Untitled.png)

Private global network is the blue line, green line represents where it can escape to the internet

![Untitled](Chapter%203%2085f44d5952f74cbbb2db5b877e32ba0d/Untitled%201.png)

## Network

- normal network
    - Routes via internet to edge location closest to destination
- Google
    - Routes so traffic enters from internet at edge closest to source
    - single global IP address can load balance worldwide

## Pricing

- Provisioned - Tell google, “Make sure youre ready to handle this load”
- Usage - “Handle whatever I use and charge me for that”
- Network traffic
    - charged on your way out of how many GB of traffic you sent

## Security

- separation of duties and physical security
- absolutely everything always encrypted at rest
- network encryption

## Scale and Automation

- scalability must be unbounded (in theory scale infinitely)
- Resource quota
    - how much of a particual service are you allowed to use
    - queryable
    
    ```jsx
    gcloud compute project-info describe --project myprojectid
    ```
    
    - tells you what your current limits are for the current project id
    

## Organization

- projects are the primary unit of organization
- every resource is owned by a particular project
- resources can be shared with other projects