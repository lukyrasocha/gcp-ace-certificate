# Feedback: what questions appeared

**Questions appeared:**

I appeared for the beta exam couple of months back, however could not pass it.

The following are my experience from the exam:

1.Lot of questions were from IAM, the questions were mostly to make sure that we have a very strong IAM knowledge. Request you to prepare a good study material for us with case based scenarios.

2.Lot of questions were also related to autoscaling and loadbalancing.

3.Questions were also to test if we were compatible and proficient with both console and GUI. A good knowledge of cloudshell is expected.

4.Almost all questions started with a small business case

Overall, it was a fantastic exam. Majority of the questions were focused on Compute Engine with a fair amount of App Engine thrown in. One needs to study compute engine in depth e.g. MIGs and how to update different kinds of updates (Yes on VMs not K8s) and how to maintain certain number of VMs etc. There were a lot of App Engine Questions and I would strongly recommend either a) Use Linux Academy Sandbox and follow tutorials. Or if possible take a Qwiklabs Subscriptions and cover their Quests which were very helpful.Understanding of K8s is very important and Kodekloud is what I used along with Nigel Poulton's videos on Acloudguru which were obviously phenomenal. IAM and associated roles for BigQuery, Security, Browser vs Viewer type of questions were there too. There were a few questions on Cloud Monitoring which I was not very sure of as there are not that many tutorials and GCP recently migrated from StackDriver as well. The resources I used were:

a) Acloudguru GCP Associate Course (via Udemy):

b) LinuxAcademy IAM and Security Course

c) Qwiklabs

d) Kodekloud (Kubernetes)

e) Cloud Advocate (Os-Login and App Engine) and AwesomeGCP YouTube channels

A few topics that i recommend reading prior to taking the exam.

- IAM
- ----Assigning roles, best practices, revoking roles ....
- ----Transferring roles between projects and organizations and what is best practice.
- ----What is best practice to migrate roles from dev/test to prod.
- ----At the virtual machine level read about cert based auth and granting access via certs
- App Engine/Kubernetes
- ----Deploying, scaling up and down
- ----reverting from one version to the other
- ----traffic routing during scaling and deploying versions of applicaiton
- ----how does does scaling work via CPU utilization and how does HTTP health check get impacted

Make sure to understand the above behaviors and how they differ for app engine vs container based deployments

Learn the commands. gcloud gsutil and bq. and

how to estimate bq command in conjunction with the estimate tool (UI)

- VPC
- ----how to get VPCs to interact
- ----Subnet IPs based on region and how do ip ranges get impacted when you have multiple region.
- ---- VPN to on premise and how does IP sharing work with your VPC.
- ---- learn about ip range calculation x.x.x.x/x ..(how to maximize and minimize number of ips in a subnet or across 2 subnet)
- ----Static ip internal vs external.
- project creation and sharing items across project.
- project billing and permission to view billing
- stack driver
- -----ingesting logs and analyzing logs in stack driver
- -----stack driver agent
- -----using stack driver to filter particular transactions
- -----watch stack driver minute videos
- DB
- when to use what type of DB or storage
- data flow. look at the biddata and iot data flow arch diagrams to understand what tools to use
- learn about dataproc and dataflow and pub/sub and how they all integrate and where items are processed and stored.

Just READ all the docs about the major offerings. they are well written and its not a bad read.

Huge bunge of questions about BigQuery, lot of things about LoadBalanding and veeery confusing ones about Reporting, Logs and so on.

So i would recommend you to focus a bit more on Logs, Reporting, Stackdriver+BigQuery etc.

- Kubernetes: There were so many in depth questions on Kubernetes. I was shocked. I knew Kubernetes from my job experience or else I would have not been able to get at least 10 questions. Don’t go to the exam until you know it inside outside. Know every detail of how you deploy and manage apps, how GCP implemented K8s services, how they interact. Basically be K8s expert.
- IAM: There were a few questions on how how you would interact between projects. For example how would one cluster accesses a resource in another project. It’s good to read best practises.
- Valid option to interact with GCP: A lot of different resources point out that there are many questions on how you perform a task, but most of the questions were looking for a valid option between GUI and gcloud
- Tricky questions: I noticed that GCP exam was trickier than AWS. A single word (project vs resource vs org) would change the answer and you had to pay attention to each word. This is apparent even in their sample exam, so just read the question.
- Time: i found time management not to be an issue even for a slow reader (English not my first Lang). I had more than an hour left on my exam.
- Watching Cloud Minute: A big thank to Mattias for introducing me to Cloud Minute. It definitely helped.

Here are some details points to cover based on the exam guide:

Understand how Google views projects

use a group, assign role to a group, add users to the group

```
understand service accounts

use IAM to add resources to IAM groups

```

Stackdriver-

```
 How to set it up for for the various services including kubernetes daemon sets

 How to collect logs, monitoring and filter data

 Understand Stack driver and its use cases for monitoring and logging for all google services not just compute. It's also your audit trail for service like Big Query.

```

Creating billing accounts -

```
 focus on how the billing export piece works.

 Creating a billing account and is easy, as is linking projects, you should know this but the logic is in the question if you read carefully.

```

Pricing:

```
 Understand how things are measured. How are prices calculated. I didn’t review this at all but I do and did understand the dataflows of how data moves, is processed, and remembered…

 You should definitely know when you use each of the compute resources

 Compute Engine (VM), Kubernetes Engine (containers), App Engine, and Google cloud launcher..

 Preemptible VMs, what is this and how can it save you money.

```

Data Storage options.

```
Cloud SQl, BigQuery, Cloud Spanner, Cloud Bigtable

The different options for Storage Multi-Regional, Regional, nearline, and coldline.

switching between the options

Accessing the data stored in each both internally and externally (with/without google accounts.

```

Load Balancers

```
 Know the two LB options and how to use them.

 Check out the advanced settings and understand health checks.

Understand sub-netting and VPC in general.

 http(s) load balancer with ssl offload.

```

Compute - understanding adding memory to an existing VM - what is the process.

SSH keys and how to use them across entire organizations.

Deploy a Kubernetes cluster and check out the options.

**launch each services and review the options.**

**Google pub/sub and how it interacts with the different compute options or doesn’t**

What are the offerings in cloud launcher.

Deployment Manager -

```
 Automate deployment of an application

 Promoting from test to prod projects

```

Section 4.

SSH to an instance, know the port, and perhaps the ports of other major services.

(RDP port)

Instance groups-- read up on these find out about maintenance settings, autoscaling, templates, multiple instance groups.

Know the CLI commands

Gcloud config configurations and why you should use them to switch between projects and how configs are global for all services in the CLI.

Kubernetes

```
 How to deploy a docker image

 Container respository

 Nodes, pods, services, deployments, statefuls sets, daemon sets. Etc..

```

App engine resources.

```
 Traffic splitting, versioning, autoscaling, reverting

 Data Solutions

 Estimating cost of Big Query

```

How each of the storage types services a purpose and why it is used.

Don’t choose a bus when you needed a smart car.

Storage classes and how they apply.

Object lifecycle management

Sharing files externally and metadata flags.

Creating a VPC with multiple subnets and with and without routing options.

Reserving static addresses

I recommend put attention to billing, IAM, GKE and App Engine. A lot of questions for these items.

I would say that 70% of the questions were related to :

Gcloud commands

Gcloud deployment manager

IAM

Kubernetes questions and knowing them in depth would probably help you pass the test.

No questions were asked on Big data services nor ML. A few questions on Cloud storage or networking only.

- You must look at the GCP Exam Guide and actually know how to most of the operations on a topic. Not just how to perform a create. But manage, modify, troubleshoot and understand the limitations. E.g. with VPCs – create a VPC, routes, subnets, instances in subnets, firewall rules, VPNs, etc. Create an GAE service, create versions, etc.
- You must take the K8s course from ACG! I wish I had, but short of that I had to read a lot from kubernetes.io and do tons of hands on myself and even then I was not 100% confident on my K8s answers. No doubt this is a huge GCP differentiator and therefore lots of K8s questions.
- My final advice: In your GCP Console, click on EVERY offered service and its sub menu systematically one by one. Read the description of the service on the page. Click on the “learn” more. Go to the service webpage, click on documentation and read the “Concepts” section for each service. Then enable the API, go create the service. Even DataProc or Spanner don’t cost much for a few minutes. You need to have both breadth and depth.

Without sharing the recollection of my exact exam questions, I can advise these topics be looked at for each exam and the appropriate lecture and GCP docs reviewed in addition to what other posts have mentioned:

**GCP-ACE**

- How to manage SSH Keys in metadata
- Managing Instance Login using OSlogin
- GAE versions and traffic splits, migrations, deployments
- Valid RFC1918 CIDR ranges
- Upgrading GKE nodes
- Tightening security on one GCE VM….. think as tight as possible using all available means for the worst user lockdown scenario
- Container Registry vs GCS
- All GKE concepts – node, pod, container, services, master, autoscaling, types of service exposure, System Objects, health checks and logs
- Cloud SQL H/A, Read Replicas and Point in Time
- New GCE sizes - some of which are not visible for trial accounts
- VPC – everything – communication in subnets across zones; regions; firewalls; routes;
- Tag vs. labels
- VPN – in great detail
- Peered VPC vs Shared – especially IAM implications
- Everything about GCS classes, lifecycle and versions
- Most of the time 2 options are easy to eliminate in the ACE exam
- No multiple answer questions for me
- Lots of IAM obviously including Cloud Identity even though you cannot setup one without an OU

**Exam Tips**

- Kubernetes , App engine and IAM -> A lot of questions related to these items.
- Deployment Manager, VPC, Load Balancer and Auto Scaling -> Some question about theses items.
- A few question about commands line.
- Learn the google console and the commands lines, **it's important**.
- Learn about the databases options, WHEN to use it and WHY to use it.
- Read the question carefully, the exam question is trick.
- Read the concepts of the services, use the google documentation.

- No questions regarding `gsutils` or `bq`
- No questions regarding Logging or Stackdriver
- 7/8 of questions on Kubernetes and AppEngine
- 6/7 questions regarding IAM
- 6/7 questions on projects/configurations or Google best practices

This may be 1/3 of the exam.

Multiple tricky networking questions, CIDR, netmask, VPC, VPC sharing , VPN and accesing resources from ProjectA to ProjectB

Also about the exam:

- no question with > 1 answers was encountered
- many questions are about setting up IAM. Concepts of setting up different kinds of roles in different levels (org/folder/project/resource) are must-know. And also knowing the best practices of setting up permissions for enterprises is very important.
- many questions about AppEngine -- the difference between Standard vs Flex. How to handle deployment, rollback, traffic-split, etc.
- also many questions about instance lifecycle -- setting up LB + managed instance group with high-availability, autoscaling, autohealing, etc. I kind of regret that I didn't review these capabilities in a more detailed way.
- some questions were also about VPC -- CIDR, subnet, and a bit routing
- setting up billing accounts and related IAM roles are also must-know
- basic understanding of k8s -- Deployments, DaemonSet, StatefulSet
- Storage and database -- need to know the difference of storage classes of GCS and the difference and use-cases of DB options.

Linux Academy practice tests (did not go thr' LA videos)

My exam had heavy focus on - Kubernetes, Gcloud commands, App Engine, IAM, SSH keys, Storage types and Network. The "Kubernetes Deep Dive" course from Nigel was really helpful.

- LinuxAcademy: ACE practice test only. I threw this in the day before the test after reading another ACG post mentioning that it was useful, and it was. I got an 80% first try, but that other 20% was new.

Test Experience:

- Difficulty was on par with AWS SysOps.
- Lots of questions on App Engine, Kubernetes, gcloud cli, and best practices as Mattias mentioned.
- Read the questions carefully for the ultimate objective and it will be easier to determine the answer.
- Over 50% of the test I answered by process of elimination identifying the wrong answers.
- Some of the questions appeared like none of the provided answers were the most efficient solution, but if you focus on the ultimate objective it helps to figure out the best answer provided.

The exam - 30 straight forward questions, 10 or so questions with multiple similar answers that need re-reading especially if English isn't your first language - double check for the one word difference which seems a bit harsh to me. A couple of questions that didn't seem to me to have a right answer and gave a bit of a headache. 10 questions that were tough, mainly IAM roles to grant access to various resources (usually logs or storage) using 'Google best practice' ie. 'least privilege'. Basic networking questions, a couple on GKE, was hoping for more GKE and less App engine.

- Google Suite vs Google Cloud Platform
- IAM, Billing Accounts, Service Accounts
- Roles, Permissions, Bindings
- Google Compute Engine
- Google Kubernetes Engine, Pods, Nodes, Deployments, Storage Classes, Security, Services, Load Balancing, etc
- AppEngine, Versions, Traffic Splitting, A/B Testing, Rollbacks
- VPC, Networking, Firewall rules, VPN
- Cloud Storage
- BigQuery, BigTable
- Cloud SQL, Cloud Spanner, Cloud Datastore
- StackDriver Logging, Debugging, Tracing, etc
- Export logs to BigQuery and lookup
- Interconnect and Peering
- Cloud Shell, Bastion Host, SSH Keys, Metadata
- Data Migration, Transfer Appliances, Transfer scheduling, etc
- Dataproc, Dataflow, Datalabs, etc
- Deployment Manager and Infrastructure as a Code
- Google Cloud Best/Recommended Practices (had few questions in Professional exams)
- Understand the CLI commands for gcloud, gsutil and kubectl, when and where to use, different options, etc

- A lot on gcloud commands and kubernetes
- A surprising amount on App Engine. Mattias, my only feedback on the course is it might be a good idea to include your walk-through of creating, deploying, modifying, and reverting an app. I get that you want us to pursue stuff on our own, but your initial guidance would be helpful.
- A fair amount on deployment manager.
- I had plenty of time to finish and review -- I marked 10 of the 50 questions for review and still finished early, so don't sweat the 2 hour time limit.

- Kubernetes course from Nigel is absolute gold
- Things observed in the exam I had focused my learning on gcloud commands as soon as I started answer a few questions based on those most of the question switched to console related so playing around in the console is highly recommended
- VVIMP - Please create an app engine walkthrough video covering the basics at least , The labs are good but doesn't say much as to what is happening beneath the surface .Found this good video explaining it _https://youtu.be/QJp6hmASstQ,
    
    Traffic splitting both by gcloud and console,Migrate ,tcp, cookie etc
    
- VPC Subnet in gcp - e.g if you are running out of ips in the subnet what to do ? what is shared vpc?
- Billing export into Bigquery
- No multiple answer questions
- Lot of questions are logic based so put the thinking cap on

most questions to least) : IAM, Kubernetes, App engine, Storage and DB dilemmas, Billing, networking, firewall and compute instances

My test seemed to be heavy on Compute Engine/Instance Groups and IAM, including questions where you needed to know which IAM role to choose.

I studied by going through both A Cloud Guru GCP courses, the Kubernetes Deep Dive. and using the A Cloud Guru exam simulator multiple times.

I also went through the LinuxAcademy course and their practice exam multiple times, and the Coursera specialization. I went through the official practice exam 3 times as well.

The last thing I did was go through each item on the Exam Guide and take a few notes for each bullet point

IAM: users, roles, services accounts, G suite, Cloud Identify, best practice

Network: quite a few questions (at least ten questions) on VPC, network, subnet, routing, VPC sharing, CIDR, HTTP load balancing

Compute: App Engine, GCE, GKE (service type), managed instances group (autoscaling, auto update)

Storage: lifecycle management, coldline, nearline

Deployment manager/Cloud Launch: 2 questions

Stackdriver: 2 questions

Project creation/billing/: about four questions

Command line: maybe eight questions or more but Matthias's course helped me to answer those questions confidently.

DB: 2-3 questions

I would recommend reading google cloud documentation (I read all links on Matthias and Nigel's courses several times), codelab helped me understand App engine, Youtube google minutes. The Google practice exam is relatively close to the actual exam (AcloudGuru practice exam is more onerous, I only got 65% last night before I took the exam this afternoon). Next.......

Hello Cloud Gurus!

I'm super happy to have passed the GCP ACE this morning! Here are a few notes on my experience:

**Study Approach:**

I studied exclusively using the ACG Google Certified Associate Cloud Engineer and Kubernetes Deepdive courses from ACG. (Most of the Kubernetes related questions were pretty straightforward after doing Nigel's course, the level of detail he provides is exactly what you need for the exam.)

I also spent quite a bit of time playing with the pricing calculator and Stackdriver logging and activity log which is worth doing as these all came up in the exam. I had no previous experience with GCP at all and followed all of the advice in the course, read all of the recommended documentation. e.g Best Practices for Organizations, Best Practice for Operating Containers, reviewed the IAM roles for all the main services etc. All of this was well worth doing. I also came across a nice overview of App Engine which is here if you haven't had much experience with it (I hadn't) [https://youtu.be/-7ml51INtEM](https://youtu.be/-7ml51INtEM)

I used the exam simulator a few times until I was getting close to 100% each time and reviewed documentation for the answers I got wrong. I used the official Google practice exam but after a couple of attempts I was getting 100%, it seemed to be quite easy but it is a good representation of the kind of questions you'll see in the exam and although it's easy it can help to expose weak areas in your understanding.

**The Exam**

The exam itself was pretty fair and tests you on everything covered in the course.

It's worth spending some time to understand the differences between the various database services (especially CloudSQL, BigTable, BigQuery) as well as Cloud Storage offerings - especially Nearline vs Coldline and when to use them.

You definitely need to understand VPCs, subnets & subnet masks, firewalls, CIDR ranges etc I had a few questions on each of those.

You don't need to memorize all the different predefined instance types but it's worth understanding them at a high level, this page has a good explanation: [https://cloud.google.com/compute/docs/machine-types](https://cloud.google.com/compute/docs/machine-types)

I saw quite a few IAM questions, especially around Service Accounts, as well as billing / billing accounts / billing export with BigQuery.

It is definitely worth getting some hands on experience with App Engine especially around deploying applications so that you understand the process (and also traffic splitting). - Same for Kubernetes. All of Nigel's course is highly relevant to the exam so well worth doing all the labs and really understanding the deployment process.

I saw quite a few questions relating to the command line so it's worth getting familiar with the command line as well as the console.

By the end of the exam I actually felt quite confident, although there were maybe around 5 questions which I'd had to guess at and didn't feel very sure about. So I was really happy to get a pass!

Unfortunately they don't give you a score and they don't publish a pass mark either so I found it a bit hard to determine whether I was ready to take the test or not... in then end I would say go with what Mattias advises and aim to be getting 100% in the ACG exam simulator and the official Google practice test and make sure you really understand why the incorrect answers are wrong and why the correct one is right!

**Focus on the exam**

1. All the storages from Google Cloud

2. K8

3. IAM Roles/Policies/Custom Roles

4. VPC/Networking/Subnet

5. Service Accounts

6. Pricing Calculator

**Exam Topic:**

1. Compute Engine

2. App Engine

3. Kubernetes Engine

4. Cloud Storage ( lifecycle management, storage classes )

5. gsutil

6. gcloud (configurations. etc))

7. IAM ( roles, etc)

8. Monitoring & Logging

9. VPC (firewalls, router,)

10. Audit / Activity logs

go through the study guide

Understand the basic structure of CIDR notation (how big or small a range is)

Understand how to separate workloads using VPC subnets and CIDR ranges

Understand how to apply least privilege principle both within the same account / project and across accounts / projects

Understand the difference between service accounts and user accounts and when to use them

Understand how to design self-healing deployments (e.g. GCE)

Understand basic Kubernetes concepts (nodes, pods, deployments - also StatefulSets, DaemonSets)

Understand how to secure credentials in Kubernetes

Understand which data solution to use in given a scenario - e.g. Cloud SQL vs. Cloud Spanner or which Cloud Storage class is most suitable

A lot of the questions were about understanding which solution to use in a given scenario. I would say you can work out the answer to most questions if you understand how GCE, GKE, IAM and the different data storage solutions work.

Topics to know for exam:

```

Cloud Storage – storage classes, versioning, object status, lifecycles

gcloud commands and gcloud configurations

AppEngine – how to split, deploy, update, migrate

Kubernetes – components understanding, kubectl commands and gcloud commands

SQL datastores – when to use: CloudSQL, Cloud Spanner, BigQuery

NoSQL datastores – when to use: Bigtable, Datastore, Cloud Firestore

VPC – SharedVPC Organization only, Custom VPC, VPC between projects, peering, VPN

Billing Account, linking to project, change billing, Exports to Cloud Storage and BigQuery

Know where you use Auto-Healing (Managed Group), Auto-Upgrade (k8s), Auto-Repair (k8s)

StackDriver monitoring, logs, exports, activity logs

SSH Key Management for One Instance and for All Instances in the Project

How to make Login to Windows Instance from console and from gcloud

Network Firewall Rules, allow/deny, priority of rules

Allowed maximal /8 and minimal /29 CIDR for Subnet

IAM, Service Accounts, Copy Role to another project

Predifined Roles for BigQuery, CloudSQL and Billing, know permissions

Permission while working with few projects and Organization
```

Familiarization with gcloud commands and Kubernetes is a must. Understand the difference between different classes of storage . the default firewalls rules created when in vpc automode and custom mode. stackdriver monitoring and logging. IAM, service accounts and roles. difference between App engine standard and flex. what to do to increase memory on a running instance.Difference between the different roles for billing.

Got questions on all the topics. Below are some which you should focus on.

AppEngine and various features of it like versioning, traffic management.

IAM and Service accounts.

Kuberenetes - deployment, service (lb, cluster and node port)

Compute Engine - CPU sizing, intel skylake, ssh configuration, service account mapping.

How do you share resources across projects.

Subnet creation and intercommunication.

gcloud config setup and basic commands (app engine, deployment manager, iam)

Gcloud market place.

Storage types (multiregion, region, coldline and nearline ) and when to use what.

- Exam is really really difficult. Do not attempt it without preparing. When you prepare , prepare in depth. Do LABS
- Exams are scenario based. So READ the question thoroughly.
- Referring to just ACloudGuru is not enough. I was following a book "Official Google Cloud Certified Associate Cloud Engineer Study Guide" by Dan Sullivan. Its a thick book, but trust me, it's worth it. Again, for each section, do labs.
- Exam was heavy on Kubernetes. So it's highly recommended that you go through the Kubernetes Deep Dive course.
- IAM heavy- Learn everything about this. Organisations, Billing, Roles, Groups, so many question grilling you on this. DO LABS
- Cloud Storage - understand the 4 storage classes and its transitions.
- Exam was heavy on Compute Engine, App Engine.
- A few question on Big Query and Cloud Spanner.
- So many questions on Google Best Practices. So Please read through it thoroughly.
- A few Questions about Networking, Cloud DNS

# **IAM**

- How to list and describe the roles using CLI.
- How to filter the roles and members using the GCP console.
- Assign permissions -> roles -> users.

Question example:

An application administrator is responsible for managing all resources in a project. She wants to delegate responsibility for several service accounts to another administrator. If additional service accounts are created, the other administrator should manage those as well. What is the best way to delegate privileges needed to manage the service accounts?

A. Grant iam.serviceAccountUser to the administrator at the project level. -> CORRECTB. Grant iam.serviceAccountUser to the administrator at the service account level.C. Grant iam.serviceProjectAccountUser to the administrator at the project level.D. Grant iam.serviceProjectAccountUser to the administrator at the service account level.

# **App Engine**

- How to deploy applications on App Engine using CLI.
- Use cases on App Engine Version functionality.
- How to split the traffic between multiple versions in the App Engine.
- When you should use Standard or flexible functionality.

Question example:

You are deploying a Python web application to GCP. The application uses only custom code and basic Python libraries. You expect to have sporadic use of the application for the foreseeable future and want to minimize both the cost of running the application and the DevOps overhead of managing the application. Which computing service is the best option for running the application?

A. Compute EngineB. App Engine standard environment -> CORRECTC. App Engine flexible environmentD. Kubernetes Engine

# **VPC — Networking**

- How to configure firewalls and use cases.
- Shared VPC.
- VPC peering vs VPN vs Interconnect.
- Firewalls
- VPN
- Types of load balancers and use cases.

Question example:

You have created several subnets. Most of them are sending logs to Stackdriver. One subnet is not sending logs. What option may have been misconfigured when creating the subnet that is not forwarding logs?

A. Flow Logs -> CORRECTB. Private IP AccessC. Stackdriver LoggingD. Variable-Length Subnet Masking

# **Projects**

- How to create projects.
- Linking projects with the billing accounts.
- How to list and describe the existing configurations.
- How to create and manage projects via CLI.

Question examples:

An app for a finance company needs access to a database and a Cloud Storage bucket. There is no predefined role that grants all the needed permissions without granting some permissions that are not needed. You decide to create a custom role. When defining custom roles, you should follow which of the following principles?

A. Rotation of dutiesB. Least principleC. Defense in depthD. Least privilege -> correct

# **Billing Accounts**

- Required roes to create and manage the billing accounts.
- Understanding the relation between Billing accounts & Projects & Organizations.
- Setting up billing exports to estimate daily/monthly charges.

Question example:

A large enterprise is planning to use GCP across a number of subdivisions. Each subdivision is managed independently and has its own budget. Most subdivisions plan to spend tensof thousands of dollars per month. How would you recommend they set up their billing account(s)?

A. Use a single self-service billing account.B. Use multiple self-service billing accounts.C. Use a single invoiced billing account.D. Use multiple invoiced billing accounts. -> CORRECT

# **Compute Engine**

- The understanding of market place uses cases.
- Auto-scaling types When to use External IP address.
- Importance of metadata and labels.
- High availability.
- Understanding Managed and Unmanaged instance groups.

Question example:

The marketing department in your company wants to deploy a web application but does not want to have to manage servers or clusters. A good option for them is:

A. Compute EngineB. Kubernetes EngineC. App Engine -> CorrectD. Cloud Functions

# **Cloud Storage (Object-based)**

- Storage classes.
- Multi-regional vs Regional vs Nearline vs Coldline.
- Changing or conversion of storage classes.
- Automatic deletion of objects and Objects transfer between the different storage classes using lifecycle policies.
- Planning and configuring data storage options (Cloud SQL, — BigQuery, Cloud Spanner, Cloud Bigtable).

Question example:

Your manager has asked for your help in reducing Cloud Storage charges. You know that some of the files stored in Cloud Storage are rarely accessed. What kind of storage would you recommend for those files?

A. NearlineB. RegionalC. Coldline -> CORRECTD. Multiregional

# **Kubernetes Engine**

- The deployment process of docker file.
- How to create a docker file and understanding of container registry.
- Autoscaling in Kubernetes.
- Deploying a container application to Google Kubernetes Engine using pods.
- Configuring Google Kubernetes Engine application monitoring and logging.

Question example:

What gcloud command will create a cluster named ch07-cluster-1 with four nodes?A. gcloud beta container clusters create ch07-cluster-1 — num-nodes=4B. gcloud container beta clusters create ch07-cluster-1 — num-nodes=4C. gcloud container clusters create ch07-cluster-1 — num-nodes=4 -> CORRECTD. gcloud beta container clusters create ch07-cluster-1 4

# **Databases**

- Relational databases: SQL vs Spanner.
- When to use BigQuery and Cloud Bigtable.
- Initializing data systems with products (e.g., Cloud SQL, — Cloud Datastore, BigQuery, Cloud Spanner, Cloud Pub/Sub, Cloud — Bigtable, Cloud Dataproc, Cloud Dataflow, Cloud Storage)
- Bigdata Tools.
- Difference between Dataproc vs Dataflow.

Question practice:

Your company’s IT department is developing a new account management application that requires transactions and the ability to perform relational database operations using fully compliant SQL. Data store options in GCP include:

A. Spanner and Cloud SQL -> CORRECTB. Datastore and BigtableC. Spanner and Cloud StorageD. Datastore and Cloud SQL

# **Stackdriver**

- Importance of Stackdriver in the Google cloud and how it works
- Creating and configuring the workspaces
- Creating Stackdriver alerts based on resource metrics
- How to add projects form different GCP accounts to single Stackdriver account via GCP console

Question example:

What is alert fatigue, and why is it a problem?

A. Too many alert notifications are sent for events that do not require human intervention, and eventually DevOps engineers begin to pay less attention to notifications. -> CORRECTB. Too many alerts put unnecessary load on your systems.C. Too few alerts leave DevOps engineers uncertain of the state of your applications andinfrastructure.D. Too many false alerts

# Links

[https://blog.devgenius.io/a-developers-guide-for-passing-google-cloud-associate-cloud-engineer-exam-8a95adb44721](https://blog.devgenius.io/a-developers-guide-for-passing-google-cloud-associate-cloud-engineer-exam-8a95adb44721)

[https://www.cloudadvocate.net/p/associate-cloud-engineer-study-notes.html](https://www.cloudadvocate.net/p/associate-cloud-engineer-study-notes.html)

[https://acloud.guru/forums/gcp-certified-associate-cloud-engineer/discussion/-Ln4gZJVvDvYIbbHY6kp/passed_google_ace_exam](https://acloud.guru/forums/gcp-certified-associate-cloud-engineer/discussion/-Ln4gZJVvDvYIbbHY6kp/passed_google_ace_exam)