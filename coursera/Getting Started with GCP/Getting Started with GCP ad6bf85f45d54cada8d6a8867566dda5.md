# Getting Started with GCP

## Learning objectives

- Identify the purpose of projects, folders, and organization nodes on Google Cloud Platform
- Describe the purpose of and use cases for Identity and Access Management
- List the methods of interacting with Google Cloud Platform
- Build a solution deployment using Cloud Launcher.

## GCP resource hierarchy

All the resources you use, whether they're virtual machines, cloud storage buckets, tables and big query or anything else in GCP are organized into projects. Optionally, these projects may be organized into folders. Folders can contain other folders. All the folders and projects used by your organization can be brought together under an organization node

![Untitled](Getting%20Started%20with%20GCP%20ad6bf85f45d54cada8d6a8867566dda5/Untitled.png)

Policies can be defined in projects, folders and organization nodes

- they are inherited downwards in the hierarchy

Each GCP project is a separate compartment and each resource belongs to exactly one

Projects can have different owners and users

Each GCP project has a name and a project ID (project ID is permanent, unchangeable across GCP) and a project number (unchangeable assigned by GCP)

### Organization node

- Top of the hierarchy
- you assign an organization policy administrator so that only people with privilege can change policies
- assign project creator role
- When you want to create folders
- When you want to apply organization wide policies centrally

![Untitled](Getting%20Started%20with%20GCP%20ad6bf85f45d54cada8d6a8867566dda5/Untitled%201.png)

![Untitled](Getting%20Started%20with%20GCP%20ad6bf85f45d54cada8d6a8867566dda5/Untitled%202.png)

![Untitled](Getting%20Started%20with%20GCP%20ad6bf85f45d54cada8d6a8867566dda5/Untitled%203.png)

## Identity and Access Management (IAM)

- lets administrators authorize who can take action on specific resources
    - “who” part and “can do what” part and “on which resource” part

### Who

- defined by google account, a service account etc.

### Can do what

- defined by an IAM role - collection of permissions
    - Primitive roles
        - owner - set up billing
        - editor - examine it and can change its state
        - viewer - examine it but not change its state
    - Predefined roles
        - defined by GCP services
        - for example InstanceAdmin
            - perform a certain set of actions on VM (listing them, reading and changing their configurations, starting and stopping them)
    - Custom roles
        - can only be used on at the project or organization level (not at the folder level)
- What if you want to give permissions to a Compute engine VM instead of a person?
    - use a service account
    
    ![Untitled](Getting%20Started%20with%20GCP%20ad6bf85f45d54cada8d6a8867566dda5/Untitled%204.png)
    
    - we can also define policies on them (for example Bob can only be a viewer to this service)
    
    ![Untitled](Getting%20Started%20with%20GCP%20ad6bf85f45d54cada8d6a8867566dda5/Untitled%205.png)
    

## Interacting with GCP

- Cloud platform console (web user interface)
    - view and manage all your projects and all the resources they use
    - enable, disable and explore the APIs of GCP services
    - gives access to cloud shell
- Cloud shell and cloud SDK (command line interface)
    - temporary VM with google cloud SDK preinstalled
    - use the tools provided by the Google Cloud Software Development kit SDK
    - Google cloud SDK - set of tools that you can use to manage your resources and your applications on GCP (gcloud tool provides the main command line interface for GCP products and services)
- Cloud Console Mobile App (For iOS and Android)
- REST-based API (for custom applications)
    - Programmatic access to products and services
    - use JSON
    - use OAuth 2.0 for authentication
    - quotas and limits (only limited amount of calls to control billing)
    - use APIs explorer
        - interactive tool that lets you easily try google APIs using a browser
        - browse quickly through different APIs and versions
    - Use client libraries to control GCP resources from within your code
        - Cloud client libraries
            - community owned hand crafted client libraries
        - Google API client libraries
            - open source generated (JAVA,python,JS,PHP,.NET...)

The services that make up GCP offer API (means that your code can use google services in much the same way that web browsers talk to web servers)

- APIs name recourses and GCP with URLs. Your code can pass information to the APIs

## Cloud marketplace (formerly cloud launcher)

- gives quick access to solutions
- pre-packaged ready to deploy solutions
    - offered by google
    - or third party vendors
- Does not update the software after its been deployed
    - you have access to the deployed systems so you can maintain them yourself

## LAMP stack

- Linux, apache, mysql, php