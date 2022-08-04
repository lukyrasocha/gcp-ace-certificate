# App engine

So we've discussed two GCP products that provide the compute infrastructure for applications: Compute Engine and Kubernetes Engine. What these have in common is that you choose the infrastructure in which your application runs. Based on virtual machines for Compute Engine and containers for Kubernetes Engine. But what if you don't want to focus on the infrastructure at all? You just want to focus on your code. That's what App Engine is for. I'll tell you more about it in this module. Let's start with PaaS. Recall that a PaaS is a platform as a service. The App Engine platform manages the hardware and networking infrastructure required to run your code. To deploy an application on App Engine, you just hand App Engine your code and the App Engine service takes care of the rest. App Engine provides you with a built-in services that many web applications need.

## App engine standard environment

- easily deploy your applications
- autoscale workloads
- free daily quota
- usage based pricing
- whats distinctive about standard environment is that low utilization applications might be able to run at no charge
- multiple languages, so you can test your app locally before you upload it to the real app engine
- simple commands for deployment
- you use a runtime provided by google (google runs your code)
- provides runtime for Java, Python, PHP and Go
- if you want other languages standard environment is not for you (use flexible environment)
- The standard environment also enforces restrictions on your code by making it run in a so called “Sandbox” - thats a software construct thats independent of the hardware, operating system, or phsyiscal location of the server it runs on.
    - it imposes some constraints:
        - your app cannot write to the local file system (it needs to write to a database service instead)
        - all requests have 60 second timeout and you cant install arbitrary third party software
        
        ![Untitled](App%20engine%20ee1eaf4d3c08492dad01ca3f17fe7009/Untitled.png)
        

## App engine flexible environment

- no sandbox constraints
- can access app engine resources
- build and deploy containerized apps with a click
- your application runs inside Docker containers on Google Compute Engine VM
- App engine manages these Compute engine machines for you
    - so you can just focus on your code
    
    ![Untitled](App%20engine%20ee1eaf4d3c08492dad01ca3f17fe7009/Untitled%201.png)
    
    ![Untitled](App%20engine%20ee1eaf4d3c08492dad01ca3f17fe7009/Untitled%202.png)
    
    ## What is an API (Application Programming Interface)
    
    What if to use that service, other pieces of software had to know internal details about how they worked? That would be a mess. So instead application developers structure the software they write so that it presents a clean, well-defined interface that abstracts away needless details and then they document that interface.
    
    ### Cloud endpoints
    
    - helps you create and maintain APIs
    - control access and validate calls with JSON Web Tokens and Google API keys
        - Identify web, mobile users with Auth0 and Firebase Authentication
    - Generate client libraries
    
    ### Apigee
    
    - helps you secure and monetize APIs
    - a platform for making APIs available to your customers and partners
    - contains analytics, monetization and a developer portal