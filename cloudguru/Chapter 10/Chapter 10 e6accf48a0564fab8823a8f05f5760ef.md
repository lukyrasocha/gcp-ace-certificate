# Chapter 10

# Security

## Proper Data Flow

- you cannot view data that you shouldnt - confidentiality
- you cannot change data that you shouldnt - integrity
- You can access data you should - availability

## How do we control data flow (AAA)

- Authentication - who are you
- Authorisation - what are you allowed to do
- Accounting - what did you do (your actions (if you view data for example) should be tracked)

## AAA data flow

User cannot directly connect to the data 

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled.png)

First you need to be authenticated to access it (so first the user connects to the AuthN) 

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%201.png)

This system will validate the identity and assign a token to them saying: “I have validated this user”

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%202.png)

This will then also talk to the accounting system to record that this user has successfully logged on

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%203.png)

The user will then connect to the application and pass on the credentials from the authentication system

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%204.png)

The application will check if the credentials are indeed assigned by the authentication system and then it will check the identity with the `AuthZ` (authorisation system), to see if this user is allowed to take this particular action (whether the action is to view, to edit some data or whatever) - if the user is in the list of `AuthZ` list of allowed users,  so it says that the action should be allowed

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%205.png)

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%206.png)

The application responds with success and that is then logged in the accounting system

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%207.png)

## What enables security in GCP

- Security products
- Security features
    - are aspects of some other things
- Security mindset
    - includes availability mindset
    - Keys:
        - Least privilege
        - Defense in depth (include layers in security)
        - Fail securely

## Key security products/features - AuthN (authentication)

Identity

- G suite,  Cloud identity
- Applications and Services use service accounts

Identity hierarchy

- google groups

## Key security products/features - AuthZ (authorisation)

Identity hierarchy (google groups)

- use groups to say who can do what

Resource hierarchy (organizations, folders,projects)

- Permissions
- Roles
- Bindings

GCS ACLs (access control list)

Billing management 

Networking structure and restrictions

## Key security products/features - Acct (accounting)

Audit / Activity logs (stackdriver) 

Billing export

- to BigQuery
- to file in GCS bucket (json or CSV)

GCS object lifecycle management

- make sure that we properly dispose sensitive material on the correct schedule

## Identity and Access Management (IAM)

### Resource Hierarchy

- Resource is something you create in GCP
- We put resources into projects (container for a set of related resources)
- We can put multiple projects inside a folder (folder can also contain subfolders)
- Organization - tied to G suite or Cloud identity domain

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%208.png)

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%209.png)

One resource can only access another one inside the same project

### IAM - permissions

- allows you to perform a certain action
- each follow the form Service.Resource.Verb
- usually correspond to REST API methods
- Examples:
    - pubsub.subscriptions.consume
    - pubsub.topics.publish
    - These permissions would allow you to get data from or publish data to a pubsub

### IAM - roles

- A role is a collection of permissions to use or manage GCP resources
- if you had all the permissions for a specific service, that would make you the administrator for that service

**Primitive roles (**project level and often too broad)

- Viewer is read only
- Editor can view and change things
- Owner can also control access and billing

**Predefined roles (give granular access to specific GCP resources)**

- e.g. roles/bigquery.dataEditor, roles/pubsub.subscriber

**Custom Role (project ore org-level collection you define of granular permissions)**

### IAM - Members

- A member is some google-known identity
- each member is identified by a unique email address
- Can be:
    - `user`: specific google account (G suite, Cloud identity, Gmail or validated email)
    - `service account`: Service account for apps/services (not used by humans)
    - `group`: Google group of users and service accounts (combine different users and service accounts together)
        - for example give all of the developers access to a specific thing
        - named collection of google accounts and service accounts
        - every group has a unique email address that is accociated with the group (developers@gmail.com)
            - you never act as the group (use the email to log in)
            - but membership in a group can grant capabilitiies to individuals
        - USE THEM FOR EVERYTHING
        - can nest groups in an organization
            - one group for each department, all those in group for all staff
    - `domain`: whole domain managed by G suite or cloud identity
        - when you want to grant access to a particular resource to every single account under a specific domain
    - `allAuthenticatedUsers`: any google account or service account
        - basically saying that the resource is public
    - `allUsers`: Anyone on the internet (Public)

### IAM - policies

- binds members to roles for some scope of resources
- who can do what to which thing
- attached to some level in the resource hierarchy
    - organization, folder, project, resource
- They are allow only - they can only allow you to do something, never deny
    - Child policies cannot restrict access granted at a higher level
    - So if you give access to someone on the organization level, thats it, they can always do that

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%2010.png)

<aside>
💡 Each resource has exactly one policy attached to it
Max 1500 member bindings per policy

</aside>

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%2011.png)

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%2012.png)

## Billing Access Control

Billing account

- represents some way to pay for GCp service usage
- Type of resrouce that lives outside of projects
- can belong to an organization (be owned by it)
- can be linked to projects (but does not own them - no impact on project IAM)

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%2013.png)

- you can have multiple billing accounts, but one project can be linked to only one billing account

### Role: Billing Account User

- purpose: link projects to billing accounts
- Level: Organization or billing account
- Use case:
    - This role has very restricted permissions so you can grant it broadly, typically in combination with Project Creator. These two roles allow a user to create new projects linked to the billing account on which the role is granted

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%2014.png)

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%2015.png)

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%2016.png)

![Untitled](Chapter%2010%20e6accf48a0564fab8823a8f05f5760ef/Untitled%2017.png)