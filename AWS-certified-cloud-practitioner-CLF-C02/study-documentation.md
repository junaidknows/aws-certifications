This file contains my study notes for the *AWS Certified Cloud Practitioner CLF-C02* course. I'll document key concepts, practical insights, and important takeaways as I progress through the course.

*Course source:* 
[AWS Certified Cloud Practitioner CLF-C02](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/?couponCode=25BBPMXACCAGE1) by [Stephane Maarek](https://www.linkedin.com/in/stephanemaarek/)
His website for discounted courses on Udemy: [Click here](https://courses.datacumulus.com/)
# What is cloud computing?

- Cloud computing is the *on-demand delivery* of computer power, database storage, applications and other IT resources
- Through a cloud services platform with pay-as-you-go pricing
- You can provision exactly the right type and size of computing resources you need
- You can grab all these resources instantly 
- A nice interface to access servers, storage, databases and a set of application services

- *AWS* owns and maintains the network-connected hardware required for these application services, while you provision and use what you need via a web application
## The deployment Models of the cloud

**Private Cloud:** A cloud services used by a single organization, not exposed to the public
- Complete control for privacy
- Security for sensitive applications
- Meet specific business needs
e.g.: *Rackspace*

**Public Cloud:**  A cloud resources owned and operated by a third-party cloud service provider delivered over the internet
e.g.: Google cloud, Amazon Web Services and Azure

**Hybrid Cloud:** Keeping some servers on premises and extend some of it's capabilities to the Cloud

## The five characteristics of Cloud Computing

- *On-demand self service:*  Users can provision resources and use them without any human interaction from AWS or provider
- *Broad network access:* Resources available over the network, and can be accessed by diverse client platforms
- *Multi-tenancy and resource pooling:* Multiple customers can share the same infrastructure and applications with security and privacy
 - Multiple customers are serviced from the same physical resources
- *Rapid elasticity and scalability:* Automatically and quickly acquire and dispose resources when needed
  - Quickly and easily scale based on demand
- *Measured Service:* Usage is measured, users pay correctly for what they have used

## Six advantages of Cloud Computing

- Trade off capital expense (**CapEx**) for operational expense (**OpEX**) 
   -  Pay-on demand: *No need to buy any sort of hardware*
   -  Reduced Total Cost of Ownership (**TCO**) & Operational Expense (**OpEX**)
- Benefit from massive economies of scale
  - Prices are reduced as AWS is more efficient due to large scale
- Stop guessing capacity
  - Scale based on actual measured usage
- Increase speed and agility
- Stop spending money running and maintaining data centers
- Go global in minutes: *leverage the AWS global infrastructure*

## Problems solved by the Cloud

- *Flexibility:* whenever we require, we can change the resources
- *Cost-Effectiveness:* pay as you go service, only pay for resources we have used
- *Scalability:* we can accommodate larger loads by making hardware stronger or adding additional nodes as required
- *High-Availability and fault-tolerance:* built across data centers around the world
- *Agility:* rapidly develop, test and launch software applications

## Different types of Cloud Computing

- Infrastructure as a Service (*IaaS*) 
   - Provide building blocks for cloud IT
   - Provides networking, computers, data storage space
   - Highest level of flexibility
   - Easy parallel with traditional on-premises IT
- Platform as a Service (*PaaS*)
   -  Removes the need for our organization to manage the underlying infrastructure 
   -  We can just focus on the deployment and management of our applications
- Software as a Service (*SaaS*)
   - Completed product that is run and managed by the service provider

![Different types of cloud computing](Different-types-of-cloud-computer1.png)

## Example of Cloud Computing Types

![](Example-of-cloud-computing-types.png)
## Pricing of the Cloud

AWS has 3 pricing fundamentals, following pay-as-you-go pricing model

- Compute: *We have to pay for the exact compute time*
- Storage: *We have to pay for the exact amount of data stored in the cloud*
- Networking: *Data transfer OUT of the Cloud*, we only pay when the data leaves the cloud, any data that goes into the cloud is free

*It solves the traditional expensive issues of IT*

More details can be found in course PDF : [[AWS Certified Cloud Practitioner Slides.pdf]]

## How to choose an AWS Region? (*exam related question*)

The answer is it depends on us but there are some factors which might change our choice. 

1. *Compliance:* with data governance and legal requirements: data never leaves a region without your explicit permissions. e.g. at times, the government wants to keep the data local to the country we're deploying the application in
2. *Proximity to customers:* It reduced latency, e.g. if our customers are in US and region is in Australia, it will increase the latency, so sometimes it better to choose the region where our customers are located to reduce *latency*
3. *Available Service within a Region:* Sometimes new services and new features aren't available in every Region 
4.  *Pricing:* Pricing varies region to region and is transparent in the service pricing page

## AWS Availability Zones

* Each region has many availability zones (*Usually 3, min is 3, max is 6*)
*Example:* For example, we take Sydney region and it's code for the region is: (*Sydney: ap-southeast-2)* 
- *ap-southeast-2a*
- *ap-southeast-2b*
- *ap-southeast-2c* 

* Each availability zone (AZ) is one ore more discrete data centers with redundant power, networking and connectivity
* They're separate from each other: so that they're isolated from disasters
* They're connected with high bandwidth, ultra-low latency networking

## AWS Points of Presence (*Edge Locations*)

- Amazon has 400+ points of presence (400+ Edge locations & 10 + Regional Caches) in 90+ cities across 40+ countries
- It's helpful when we deliver content to end users with lower latency

**Note:** 
AWS services vary by region, and not all services are available in every region. If a particular service is unavailable in your selected region, you can verify its regional availability by consulting the [AWS Global Infrastructure page](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

## Shared Responsibility Model Diagram (*exam related question*)

It's basically our responsibility vs AWS when using the their cloud services

1. We as customers, we are responsible for the security *in the cloud*, from usage to configuration, security, data, operating systems, our network, firewall configuration etc, it's on us
2. *AWS* is responsibility for the *security of the cloud*, all the hardware, all the software, all their own internal security
3. That's why we do have this shared responsibility 

# IAM: Users & Groups

- IAM stands for *identity and Access management, **Global** service*
- *Root account is created by default*, it shouldn't be used or shared with anyone
- *Users* are people within your organization and can be grouped, even can belong to multiple groups
- Groups only contain users and groups cannot be created within a group
- Users don't have to belong to a group can work on it's own and user can belong to multiple groups
## IAM: Permissions

- Users or Groups can be assigned JSON documents called policies. e.g:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": [
                "arn:aws:s3:::my-secure-bucket",
                "arn:aws:s3:::my-secure-bucket/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:StartInstances",
                "ec2:StopInstances",
                "ec2:DescribeInstances"
            ],
            "Resource": "arn:aws:ec2:us-east-1:123456789012:instance/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "rds:DescribeDBInstances",
                "rds:StartDBInstance",
                "rds:StopDBInstance"
            ],
            "Resource": "arn:aws:rds:us-east-1:123456789012:db:mydatabase"
        }
    ]
}
```

- These policies define the permissions of the users
- In AWS you apply the least privilege principle don't give more permissions than a user need because if a user have more permissions and they turn on some instances that can cause companies big bills 
- IAM is a global service, so its not based on it's region but some other services do
- We need to create users, why? Because using root account is not a best practice
- *Tags* are used everywhere in AWS, it allow use to give metadata to our resources
## IAM Policies inheritance

Example how policies are inherited:

If there's a group of developers and operations, both groups have their own policies for permissions. However if a guy who belongs to Audit team get added to these 2 groups, he will inherit all the permission policies from all 3 groups. 

- *Inline policy:* it's a policy only attached to the user who's not the part of any group
### IAM Policies Structure

- *Consists of*:
  - *Version: policy language* , always include "2012-10-17"
  - *Id:* an identifier for the policy (optional)
  - *Statement:* one or more individual statements (required)
- *Statements consists of:*
  - Sid: an identifier for the statement (optional)
  - Effect: whether the statement allows or denies access (allow, deny)
  - Principle: account/user/role to which this policy applied to
  - Action: list of actions this policy allows or denies
  - Resource: list of resources to which the actions applied to
  - Condition: conditions for when this policy is in effect (optional)

**Refer to**: Course slides for example of *json file which shows the structure of policy in code*

Tip: * star means in *AWS* anything that means any action on any resource is exactly like giving administrator rights to some

### IAM MFA
#### IAM- Password Policy
- Strong passwords = higher security for your account
- In AWS, we can setup a password policy which allow us:
 - Set a minimum password length
 - We can request specific character types 
   - including UPPERCASE letters
   - lowercase letters
   - Numbers 
   - non-alphanumeric characters i.e. *# $ % ^ & *  !* 
- We can allow all IAM users to change their own password once they use the generic ones to login for the first time
- We can prevent reuse of the same password as extra layer of security
- Password expiry (*User password will be expired in 30 days or 90 days or 180 days*) 
#### Multi-Factor Authentication - MFA

- AWS makes it mandatory to use MFA as a additional security layer and it's 100% recommended to use it
- Of course we need to make sure our root accounts and all our IAM users are using MFA to protect their accounts
- Users have access to your account and they possibly can make some changes to the configurations or delete some of resources in your AWS account
-  MFA is basically a combination of the password we set up along with a security device i.e. our phones with some sort of authenticator app running on it (Virtual MFA device). i.e. *Microsoft Authenticator, Google Authenticator, Authy or any 3rd party authenticators* or we can use a *Universal 2nd Factor (U2F) Security key by YubiKey* 
- We also have *Hardware Key Fob MFA device*: **Provided by Gemalto** (*Third party*)
- Hardware Key Fob MFA device for AWS GovCloud (US government) *Provided by SurePassID* which is also a (*3rd party*) 
- MFA generates new tokens every 30 seconds so we are not using the same code to get into our account, makes the accounts extra secure rather than just having password
- One of it's main *benefits are:* if someone has your password or it's stolen, they can use it to log in but MFA won't allow them to go past that stage so that means your account is not compromised
### Accessing AWS
*To access AWS we have three options:*
 - AWS management console (which is protected by password along with MFA)
 - We also have command line interface (CLI) which we can set up directly on our machines and are protected by *access keys*, this will allow us to access AWS from our terminal directly
 - The last one is *AWS Software Developer Kit (SDK)* which is used when we have to call API's from AWS from within our application code, this is also protected by *access keys*
### How to generate access keys?
 
 - Access keys are generated through the *AWS Console*
 - Every user manage their own access keys
 - Access keys are secret, just like our passwords, *Never share them with anyone*
 
 Access Key ID = *Username*
 Secret Access Key = *Password*

Once we have access key id and secret access key, we need to load that up in our command line interface on our machine
### What's the AWS CLI?

- It's a tool on our computer usually use to get tasks done by running commands on our machine
- We can interact with AWS services through command line interface by using commands or you can even say by running some codes
- *It's called AWS CLI:* because when we write commands in CLI, it starts from *~ aws* 
- With this, we get direct access to the public *APIs* of our AWS services
- We can develop some scripts to manage our resources and of course can automate certain tasks using those scripts
- AWS cli is open-source and can be founded on GitHub
- AWS CLI is an alternative to *AWS Management Console*
### What's the AWS SDK?

- It's a AWS Software Development kit *(AWS SDK)*
- It's a set of libraries which are *Language-specific APIs*
- It will also allow us to enable *AWS services programmatically*
- SDK is not something we use in our terminal but instead we Embed it within our application which we have to code
- It supports so many different programming languages like (*Python, Java, JavaScript, .NET, Ruby, Go, Node.js, C++ etc)
- It also supports mobile SDks i.e. *IOS or Android*
- And Internet of Things devices in case we are using some thermal sensors or some bike locks that are connected, all these kind of things

A good example given by Stephen (Instructor of this course)
```markdown
AWS CLI is built on AWS SDK for Python dubbed as **BOTO***
```

To install *AWS CLI* on any machine, we can just go to this AWS official documentation: [AWS CLI Installation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
	*Note:* If we need to update the version of CLI, we just need to reinstall it through the installer we download from the documentation

### AWS CloudShell

AWS CloudShell is an alternative *command-line* interface that runs directly within the AWS web browser. However, if it is not visible, ensure that you are in the correct AWS region, as CloudShell is not available in all regions.

### IAM Roles for Services

IAM (Identity and Access Management) **roles for services** in AWS allow AWS services (like EC2, Lambda, etc.) to interact with other AWS services **securely** without needing to store or manually manage access credentials (like usernames or passwords)
#### **How It Works?**

- Instead of attaching an **IAM User with access keys**, AWS uses **IAM Roles** to provide permissions
- When a service (e.g., EC2) assumes a role, AWS automatically provides **temporary security credentials** to that service
- The service can then use these credentials to interact with other AWS services securely
- *A role is a way to give AWS entities permissions to do stuff on AWS*
 - When we go to create a role in *IAM*, we can see 5 type of different trusted entity types from where we will choose *AWS SERVICE entity* for exam point of view and this course

### IAM Security Tools
#### IAM Credentials Report (account-level)
- A report that lists all your account's users and the status of their various credentials
- Very helpful to check which user require our attention from a security standpoint e.g. if a user hasn't changed his password for over 6 months. 
#### IAM Access Advisor (user-level) *New name: LastAccess*
- Also known as *IAM Security Advisor*
- Access advisor shows the service permissions granted to a user and when those services were last accessed
- You can use this information to revise your policies
	- To access LastAccess, we will go to *users* and select the user and last tab is *LastAccess* which we will access to see which services were accessed by my user and exactly when

### IAM Guidelines & Some Best Practices

- Don't use the root account except for AWS account setup or something which can't be done without a root account
- One physical user should only have *One AWS account* unless for administrative purposes
- Assign users to groups and assign permissions to groups rather than assigning permissions to individuals
- Create strong password policies
- Use and enforce the use of *MFA*
- Create and use *Roles* for granting permissions to AWS services
- Use Access Keys for Programmatic Access (*CLI / SDK*)
- Audit permissions of your account using *IAM Credentials Report & IAM LastAccess* (*Access Advisor* old name)
- Never ever share IAM users & Access Keys
### Shared Responsibility Model for IAM (*v.imp for Exam*)

| AWS responsibility                       | Our Responsibility                                            |
| ---------------------------------------- | ------------------------------------------------------------- |
| Infrastructure (global network security) | Users, Groups, Roles, Policies, management and monitoring     |
| Configuration and vulnerability analysis | Enable MFA on all accounts created                            |
| Compliance validation                    | Make sure the keys are rotated often                          |
|                                          | Use IAM tools to apply appropriate permissions                |
|                                          | Analyze access patterns & review permissions in your accounts |

-------------
# EC2 Elastic Compute Cloud
## Amazon EC2

- EC2 is one of the most popular of AWS offerings
- EC2 = Elastic Compute Cloud = Infrastructure as a Service
- It mainly consists in the capability of: 
 - Renting Virtual Machines (EC2)
 - Storing data on virtual drives (EBS)
 - We can distribute load acrss machines (ELB)
 - We can scale the services using an auto-scaling group (ASG)
- *Knowing EC2 is fundamental to understand how the Cloud works because cloud is just another computer sitting somewhere which we rent according to our needs*
### EC2 sizing & configuration options

- Operating System (OS): *Linux, Windows or Mac OS*
- How much compute power & cores (*CPU*)
- How much random-access memory (*RAM*)
- How much storage space:
 - Network-attached (*EBS & EFS*)
 - Hardware (EC2 instance store)
- Network card: how much speed we require, public IP address
- Firewall rules: Security groups
- *Bootstrap script (configure at first launch): EC2 User Data*
#### EC2 User Data

- It is possible to bootstrap our instances to use an *EC2 User data* script
- *bootstrapping* means launching commands when a machine starts
- The script only *run once* at the instance *first start*
- EC2 user data is used to automate boot tasks such as:
  - Installing updates
  - Installing software
  - Downloading common files from the internet
  - Anything we can think of
  - *Adding more tasks to bootstrap means more loading of boot time*
- *The EC2 User data script runs with the root user only* 
### EC2 Instance Types - *General Purpose* (Imp for exam)
- Great for diversity of workloads like web servers or code repositories
- Good balance between: 
 - Compute
 - Memory
 - Networking
- For this course, we will be focusing on t2.micro which is a *general purpose EC2 instance*
- Amazon naming convention works in the following way: 
```python
For example: m5.2xlarge

m: #instance class
5: #generation (AWS imrpoves them over time, changes the hardware)
2xlarge: #size within the instance class like ram, cpu, storage etc
```

### EC2 Instance Types - *Compute Optimised* 

- Great for computer-intensive tasks that require high performance processors:
 - Batch processing workloads
 - Media transcoding
 - High performance web servers
 - High performance computing (*HPC*)
 - Scientific modeling & machine learning
 - Dedicated gaming servers
 *All the compute instances are of C names e.g. C5, C6 and so on..*
### EC2 Instance Types - *Memory Optimised*

- Fast performance for workloads that process large data sets in memory
- Use cases: 
 - High performance, relational/non-relational databases
 - Distributed web scale cache stores
 - In-memory databases optimised for BI (business intelligence)
 - Applications performing real-time processing of big unstructured data
 *For memory optimised instances it will be R names series because R stands for RAM but there also going to be X1 or Z1 for high memory instances*

### EC2 Instance Types - *Storage Optimised*

- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- *Use Cases:*
 - High frequency online transaction processing (OLTP) systems
 - Relational & NoSQL databases
 - Cache for in-memory databases (for example, Redis)
 - Data warehousing applications
 - Distributed file systems
--- 
# Introduction to Security Groups

- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of our *EC2* instances
- Security groups are like *firewalls* in cloud which controls what traffic can enter EC2 instance and what outbound traffic can EC2 instance perform to access internet
- Security groups only contain *allow* rules
- Security groups rules can reference by IP or by security group

## Security Groups (*Deeper Dive*)

- Security groups are acting as firewall on EC2 instances
- They regulate:
 - Access to Ports
 - Authorised IP ranges - IPv4 and IPv6
 - Control of inbound network (*from outside to the instance*)
 - Control of outbound network (*from the instance to other*)

**Note:** Anytime we see timeout accessing our server for example if we try to SSH into our server or even a simple browsing to our server, the time out is because there is something wrong with the security groups rules as a firewall, so we always investigate it

### Classic Ports (*Important for Exam*)

- 22 = SSH (Secure Shell) - log into a Linux instance
- 21 = FTP (File Transfer Protocol) - upload files into a file share
- 22 = SFTP (Secure File Transfer Protocol) - upload files using SSH
- 80 = HTTP - access unsecured websites
- 443 = HTTPS - access secured websites
- 3389 = RDP (Remote Desktop Protocol) - log into a Windows Instance

#### SSH into EC2 instance linux method:

1. Download secret key for our instance e.g. *EC2*
2. Put the download .pem file into the working directory
3. Once it's done, use the following command to get into EC2 through SSH
```SSH
ssh -i EC2-First\ Instance.pem ec2-user@3.25.172.105

#We use ec2-user and ipv4 public address of our instance to login
```
4. If we get an error like *Unprotected file* , we use the following command to authenticate the key
```SSH

chmod 0400 EC2-first-instance.pem #We replace the file name with our actual key file name

Once it's authenticated we can run the above command to log in
```

#### EC2 Instance Connect - Direct Access Through Browser

1. Just go to our instances
2. Click connect
3. And that's it
4. If EC2 instance connect ask for our configuration e.g. access key or secret access key *never ever enter those in any EC2 instances as a rule of thumb otherwise it will be visible to other account holders using that instance*
5. Instead we will use *IAM Roles*
6. So for example: we create one IAM Role for EC2 service with Iamready only access policy attached to it
7. We will go to our instances *EC2* , we select our instance, we click *action* tab then head to *security section*
8. In *security* section we will click *modify IAM role* and select the role we created for this instance
9. It will give it the configuration instead of us doing it which is not ideal in this case
10. This is how we provide the AWS configuration credential through *IAM* Roles always

*Note:* Use IAM roles always for *EC2 instances*

## EC2 Instances Purchasing Options

- On-Demand Instances: short workload, predictable pricing, pay by second
- Reserved (*1 & 3 years*)
   - Reserved Instances - long workloads
   - Convertible Reserved Instances - long workloads with flexible instances
- Saving Plans (*1 & 3 years*) - commitment to an amount of usage, long workload
- Spot Instances - short workloads, cheap, can lose instances (*less reliable*)
- Dedicated Hosts - book an entire physical server, control instance placement
- Dedicated Instances - no other customers will share your hardware
- Capacity Resources - reserver capacity in specific AZ for any duration

### EC2 on Demand

-  Pay for what we use:
  -  Linux or Windows- billing per second, after the first minute
  - All other operating systems - billing per hour
- Has the highest cost but no upfront payment
- No long-term commitment
*Recommended for short-term and uninterrupted workloads, where you can't predict how the application will behave*

Can always refer to course slides for detailed purchasing options [[AWS Certified Cloud Practitioner Slides.pdf]]

### Which option is good for me? (*As beginner*)

##### We can think of all the pricing for like it's a resort 
- *On demand:* coming and staying in like a resort whenever we like, we pay the full price
- *Reserved:* like planning ahead and if we plan to stay for a long time, we may get a good discount
- *Savings Plans:* pay a certain amount per hour for certain period and stay in any room type (e.g. King, Suite, Sea View..)
- *Spot Instances:* the hotel allows people to bid for the empty rooms and the highest bidder keeps the rooms. you can get kicked out at any time
- *Dedicated Hosts:* we book an entire building of the resort
- *Capacity Reservations:* you book a room for a period with full price even you don't stay in it
---
# EC2 Instance Storage

## What's an EBS Volume?
- An *EBS (Elastic Block Store) Volume* is a *network* drive you can attach your instances while they run
- it allows your instances to persist data, even after their termination
- They can only be mounted to one instance at a time (at Certified Cloud Practitioner level)
- They are bound to a specific availability zone

*Analogy:* We can think of it as network USB stick, which we can take it out from one computer to another computer

*Free tier:* 30 GB of free EBS storage of type General Purpose (SSD) or Magnetic per month
### EBS - Delete on Termination attribute *(imp for exam)*

- Controls the EBS behaviour when an EC2 instance terminates
   - By default, the root *EBS volume* is deleted (*attribute enabled*)
   - By default, any other attached *EBS volume* is not deleted (*attribute disabled*)
- This can be controlled by the *AWS console* / *AWS CLI*
- *Use case:* preserve root volume when instance is terminated
### EBS Snapshots

- Make a backup (snapshot) of your *EBS Volume* at a point in time
- Not necessary to detach volume to do snapshot, but recommended
- Can copy snapshots across *AZ or Region*
#### EBS Snapshots Features
- *EBS Snapshot Archive:*
  - Move a Snapshot to an "archive-tier" that is 75% cheaper
  - Takes within 24 to 72 hours for restoring the archive
- *Recycle Bin for EBS Snapshots*
   - Setup rules to retain deleted snapshots so you can recover them after an accidental deletion
   - Specify retention (*from day 1 to 1 year*) It protects us against accidental deletion
### AMI 
- *AMI:* Amazon Machine Image
- AMI are the *customisation of en EC2 instance*
   - You add your own software, configuration, operating system, monitoring..
   - Faster boot/ configuration time because all your software is pre-packaged
- AMI are built for a specific region (and can be copied across regions)
- You can launch EC2 instances from:
   - A Public AMI: *AWS* provided
   - *Your own AMI:* you make and maintain them yourself
   - *An AWS Marketplace AMI:* an AMI someone else made (and potentially sells)
### AMI Process (*from an EC2 instance*)

- Start an EC2 instance and customise it i.e. *installing linux packages or deploy softwares in windows servers*
- Stop the instance (*for data integrity*)
- Build an AMI - this will also create EBS snapshots
- Launch instances from other *AMIs*

### EC2 image builder
- Used to automate the creation of Virtual Machines or container images
- -> Automate the creation, maintain, validate and test EC2 AMIs
- Can be run on a schedule ( weekly, whenever packages are updated etc)
- Free service (only pay for the underlying resources which means we only pay when the image is created, stored somewhere on cloud and distributed)
### EC2 Instance Store
- EBS volumes are network drives with good but "limited" performance
- If you need a high performance hardware disk, use **EC2 Instance Store**
##### Why we use Instance Store?
- To have better performance for I/O
- EC2 Instance Store lose their storage if they're stopped that's why it's also called *ephemeral* storage as well so that means that EC2 Instance store can not be used as a durable long term place to store your data. 
- Good for buffer / cache / scratch data / temporary content that's it nut for long run, use EBS for long run for better protection of data
- Risk of data loss if hardware fails of Instance Store
- Backups and Replication correctly are our responsibility

### EFS - Elastic File System
- Managed NFS (network file system) that can be mounted on 100s of EC2
- EFS works with *Linux EC2 only* instances in multi availability zones
- Highly available, scalable, expensive 3 times of gp2 storage, pay only upon usage, no capacity planning that means if we use 20GB, we only pay for 20GB of storage
### EFS Infrequent Access (EFS-IA) (*Imp for exam*)
- A *storage class* that is cost-optimised for files not accessed every day
- Up to 92% lower cost compared to *EFS standard* which is another storage class
- EFS will automatically move your files to EFS-IA based on the last time they were accessed but we need to *Enable EFS-IA* with a Lifecycle Policy
*Example:* Move files that are not accessed for 60 days to EFS-IA storage that will be cost savings because it's almost 92% lower cost than EFS standard. All this happens automatically
- It's very transparent to the applications access EFS, no one will know because it all happens behind the scenes, users can access those files anytime again without any problem

### Shared Responsibility Model for EC2 Storage

*AWS Responsibility* : 
- Their Infrastructure
- Replication for data for EBS volumes & EFS, so if anytime their's any issues with the hardware the customers are not impacted
- Replacing faulty hardware
- Ensuing their employees cannot access your data

*Customers Responsibility:*
- Setting up backup / snapshot procedures
- Setting up data encryption
- Responsibility of any data on the drives
- Understanding the risk of using EC2 Instance Store
### Amazon FSx 

- Launch 3rd party high-performance file systems on AWS
- Fully managed service

**Amazon FSx for Windows File Server**
- Amazon FSx is the way to deploy FSx for Windows File server over SMB protocol or Windows NTFS storage protocols
- Our client can access this file server over SMB or even our instances within the same region
- Integrated with Microsoft Active Directory
- It can be directly access from AWS or from on-prem infrastructure
**Amazon FSx for Lustre**
- A fully managed, high-performance Linux file system, scalable file storage for *High Performance Computing (HPC)*
- The name *Lustre* is derived from "Linux" and "Cluster"
- It's mainly for Machine Learning, Analytics, Video Processing, Financial Modeling
- Scales up to 100s GB/s millions of IOPS, sub-ms latencies
---
# ELB & ASG - Elastic Load Balancing & Auto Scalling Groups

## High availability , Scalability, Elasticity
- Scalability means that an application / system can handle greater loads by adapting
- There are two kinds of scalability:
  - Vertical Scalability
  - Horizontal Scalability (*= elasticity*)
- Scalability is linked but different to High Availability
### Vertical Scalability
- Vertical Scalability means increasing the size of the instance
- For example: *your application runs on a t2.micro*
- Scaling that application vertically means running it on a t2.large
- Vertical scalability is very common for non distributed systems, such as a database
- There's usually a limit to how much you can vertically scale (*hardware limit)*
### Horizontal Scalability
- Horizontal Scalability means increasing the number of instances / systems for your application
- Horizontal scaling implies distributed systems
- This is very common for web applications / modern applications
- When we design something we keep horizontal scalability in mind
- It's easy to horizontally scale thanks the cloud offerings such as *Amazon EC2*
### High availability
- High availability usually goes hand in hand with horizontal scaling
- High availability means running your application system in at least 2 different availability zones like a failover cluster
- The goal of high availability is to survive a data centre loss (*disaster*) e.g. Earthquake, Tsunami, Power Outage
### High Availability & Scalability for EC2
- **Vertical Scaling:** Increase instance size (*= scale up /down*)
 - From: *t2.nano - 0.5G of RAM, 1 vCPU*
 - To: *u-12tb1.metal - 12.3TB of RAM, 448 vCPUs*
- **Horizontal Scaling:** Increase number of instances (*= scale out/ in*)
  - Auto Scaling Group
  - Load Balancer
- **High Availability:** *Run instances for the same application across multi availability zones*
  - Auto Scaling Group multi AZ
  - Load Balancer multi AZ
### Scalability vs Elasticity (vs Agility) *(imp for exam)*

- ﻿﻿*Scalability:* Ability to accommodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale out)
- ﻿﻿*Elasticity:* once a system is scalable, elasticity means that there will be some "auto-scaling" so that the system can scale based on the load. This is "cloud-friendly": pay-per-use, match demand, optimize costs
- ﻿﻿*Agility:* (not related to scalability - distractor) new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes.

### Why use an Elastic Load Balancer?

- ﻿﻿An ELB (Elastic Load Balancer) is a managed load balancer
  - ﻿﻿AWS guarantees that it will be working
  - ﻿﻿AWS takes care of upgrades, maintenance, high availability
  - ﻿﻿AWS provides only a few configuration knobs
- ﻿﻿It costs less to setup your own load balancer but it will be a lot more effort on your end (maintenance, integrations)
- 4 kinds of load balancers offered by AWS:
- Application Load Balancer (TTP / HTTPS only) — Layer 7
- ﻿﻿Network Load Balancer (ultra-high performance, allows for TCP) - Layer 4
- ﻿﻿Gateway Load Balancer - Layer 3
- ﻿﻿Classic Load Balancer (retired in 2023) — Layer 4 & 7

In Depth diagram for all 3 different type of load balancers can be found in this pdf: [[AWS Certified Cloud Practitioner Slides.pdf]]

### How do we create load balancers automatically in the back end? 
### *We will use Auto Scaling Group*

- In real-life, the load on our websites and application can change
- ﻿﻿In the cloud, you can create and get rid of servers very quickly
- ﻿﻿The goal of an Auto Scaling Group (ASG) is to:
  - ﻿﻿Scale out (add EC2 instances) to match an increased load
  - ﻿﻿Scale in (remove EC2 instances) to match a decreased load
  - ﻿﻿Ensure we have a minimum and a maximum number of machines running
  - ﻿﻿Automatically register new instances to a load balancer
  - ﻿﻿Replace unhealthy instances
- *Cost Savings:* only run at an optimal capacity (principle of the cloud)
### Auto Scaling Groups - Scaling Strategies

- ﻿﻿Manual Scaling: Update the size of an ASG manually

- ﻿﻿Dynamic Scaling: Respond to changing demand
  - ﻿**Simple / Step Scaling***
    - ﻿﻿When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
    - ﻿﻿When a CloudWatch alarm is triggered (example CPU < 30%), then remove |
- ﻿﻿**Target Tracking Scaling**
   - ﻿﻿Example: I want the average ASG CPU to stay at around 40%
-  ﻿﻿**Scheduled Scaling:**
   - ﻿﻿Anticipate a scaling based on known usage patterns
   - ﻿﻿Example: *increase the min. capacity to 10 at 5 pm on Fridays*
- *Predictive Scaling:* Uses machine learning to predict the future traffic ahead of time by using patterns of customers visiting our website in the past
    - Automatically provisions the right number of EC2 instances in advance

 *Useful when your load has predictable time-based patterns*

---
# Amazon S3

## Introduction
- Amazon S3 is one of the main building blocks of AWS
- It's advertised as "infinitely scaling" storage
- Many websites use Amazon S3 as backbone
- Many AWS services use Amazon S3 as an integration as well

## Amazon S3 use cases
- Backup and storage
- Disaster Recovery
- Archive
- Hybrid Cloud Storage
- Application hosting
- Media hosting
- Data leaks & big data analytics
- Software delivery
- Static website
Examples: *Nasdaq stores 7 years of data into S3 Glacier* and Sysco runs analytics on its data and gain business insights

## Amazon S3 - Buckets

- ﻿﻿Amazon S3 allows people to store objects (files) in "buckets" (directories)
- ﻿﻿Buckets must have a globally unique name (across all regions all accounts)
- ﻿﻿Buckets are defined at the region level
- ﻿﻿S3 looks like a global service but buckets are created in a region
- ﻿﻿Naming convention
   - ﻿﻿No uppercase, No underscore
   - ﻿﻿3-63 characters long
   - ﻿﻿Not an IP
   - ﻿﻿Must start with lowercase letter or number
   - ﻿﻿Must NOT start with the prefix xn--

**S3 Bucket**

*Must NOT end with the suffix -salias*

## Amazon S3 - Objects

- ﻿﻿Objects (files) have a Key
- ﻿﻿The key is the FULL path:
    - ﻿﻿s3://my-bucket/my_file.txt
    - ﻿﻿s3://my-bucket/my_folderl/another_folder/my_file.txt
- ﻿﻿The key is composed of prefix + object name
   - ﻿﻿s3://my-bucket/my_folder|/another_folder/my_file.txt
- ﻿﻿There's no concept of "directories" within buckets (although the Ul will trick you to think otherwise)
- ﻿﻿Just keys with very long names that contain slashes ("/")
- ﻿﻿Object values are the content of the body:
    - ﻿﻿Max. Object Size is 5 TB (5000GB)
    - ﻿﻿If uploading more than 5GB, must use "multi-part upload"
- ﻿﻿Metadata (list of text key / value pairs - system or user metadata)
- ﻿﻿Tags (Unicode key / value pair - up to 10) - useful for security / lifecycle
- ﻿﻿Version ID (if versioning is enabled)

## Amazon S3 - Security

- ﻿﻿User-Based
  - ﻿﻿IAM Policies — which API calls should be allowed for a specific user from IAM
- ﻿﻿Resource-Based
  - ﻿﻿Bucket Policies - bucket wide rules from the S3 console - allows cross account
  - ﻿﻿Object Access Control List (ACL) - finer grain (can be disabled)
  - ﻿﻿Bucket Access Control List (ACL) - less common (can be disabled)
- ﻿﻿*Note:* an IAM principal can access an S3 object if
  - ﻿﻿The user IAM permissions ALLOW it OR the resource policy ALLOWS it.
  - ﻿﻿AND there's no explicit DENY
- ﻿﻿*Encryption:* encrypt objects in Amazon S3 using encryption keys

## S3 Bucket Policies

- ﻿﻿**JSON based policies**
  - ﻿﻿Resources: buckets and objects
  - ﻿﻿Effect: Allow / Deny
  - ﻿﻿Actions: Set of APl to Allow or Deny
  - ﻿﻿Principal: The account or user to apply the policy to


- **Use S3 bucket for policy to:**
  - ﻿﻿Grant public access to the bucket
  - ﻿﻿Force objects to be encrypted at upload
 - ﻿﻿Grant access to another account (Cross  
    Account)

Example of the json file:
```json
"Version": "2012-10-17",

"Statement": [

{

"Sid": "PublicRead",

"Effect": "Allow",

"Principal": "*",

"Action": [

"s3: GetObject"

1, "Resource": [

"arn:aws:s3:::examplebucket/*"
 ]
 }
    ]
}
```

When we create the S3 bucket policies to make it publicly available we can use aws s3 policy generator. 

1. Select policy type : *S3 bucket policy*
2. Principle we will add * (that means get everything)
3. Actions: *Get object* (from the dropdown list)
4. Amazon Resource name (ARN): we can copy this from our bucket name and at the end of the bucket name we will add /*
5. Now hit Generate Policy
6. Once the policy is generated we will just paste it in the bucket policies

## Amazon S3 - Static Website Hosting

- S3 can host static websites have have them accessible on the internet
## Amazon S3 - Versioning

- ﻿﻿You can version your files in Amazon S3
- ﻿﻿It is enabled at the bucket level
- ﻿﻿Same key overwrite will change the "version": 1, 2, 3....
- ﻿﻿It is best practice to version your buckets
  - ﻿﻿Protect against unintended deletes (ability to restore a version)
  - ﻿﻿Easy roll back to previous version
*Notes:*
- ﻿﻿Any file that is not versioned prior to enabling versioning will have version "null"
- ﻿﻿Suspending versioning does not delete the previous versions
## Amazon S3 - Replication (CRR & SRR)

- **CRR:** Cross-region replication
- **SRR:** Same region replication

*The main purpose of this is having one bucket in one region and another bucket in another region* and we need to set up *asynchronous replication*

To do that, we need to ensure:
- Must enable Versioning in source and destination buckets
- If we choose *CRR*, the two regions will be different
- If we choose *SRR*, the two regions will be the same
- It's possible to have these buckets with different *AWS accounts*
- Copying is asynchronous
- To make replication work, you must give proper IAM permissions to S3, so it has permissions to read and write

## S3 Storage Classes (*important for exam*)

- ﻿﻿Amazon S3 Standard - General Purpose
- ﻿﻿Amazon S3 Standard-Infrequent Access (IA)
- ﻿﻿Amazon S3 One Zone-Infrequent Access
- ﻿﻿Amazon S3 Glacier Instant Retrieval
- ﻿﻿Amazon S3 Glacier Flexible Retrieval
- ﻿﻿Amazon S3 Glacier Deep Archive
- ﻿﻿Amazon S3 Intelligent Tiering

For in depth refer to: [[AWS Certified Cloud Practitioner Slides.pdf]]
## S3 Durability and Availability

**Durability:**
  - ﻿﻿High durability (99.999999999%, 1 1 9's) of objects across multiple AZ
  - ﻿﻿If you store 10,000,000 objects with Amazon S3, you can on average expect to incur a loss of a single object once every 10,000 years
  - ﻿﻿Same for all storage classes
  **Availability:**
  - ﻿﻿Measures how readily available a service is
  - ﻿﻿Varies depending on storage class
  
*Example:* S3 standard has 99.99% availability = not available 53 minutes a year
## S3 Standard - General Purpose

- ﻿﻿99.99% Availability
- ﻿﻿Used for frequently accessed data
- ﻿﻿Low latency and high throughput
- ﻿﻿Sustain 2 concurrent facility failures

*Use Cases:* Big Data analytics, mobile & gaming applications, content distribution

**Note:** 
*When selecting any of these classes, we will first upload the data. Before completing the upload, we will navigate to the file's properties to specify the appropriate class based on our requirements within the bucket.* *We can also modify the storage class of an item that has already been uploaded to the bucket.* We can even automate moving these objects to different classes by creating it's life cycle rule, under the management tab of our file. 
## S3 Encryption (*imp exam*)
There's 2 type of encryption which we can look at for S3 buckets:
**Server-side encryption** (*Default*)
When the user uploads the file, the server encrypts the file after receiving it by default it's always on

**Client-side encryption**
When the user *encrypts* the file before uploading to a Amazon bucket S3
## IAM Access Analyzer for S3 
- It make sures that only intended people have access to our S3 buckets
*Example:* publicly accessible bucket, bucket shared with other AWS account
- It evaluates S3 bucket policies, S3 ACLs, S3 Access Point Policies
- Powered by IAM Access Analyzer
## Shared Responsibility Model for S3

*By AWS:*
- Infrastructure, (global security, durability, availability, sustain concurrent loss of data in two facilities)
- Configuration and vulnerability analysis
- Compliance Validation

*By Us (client side):*
- S3 Versioning
- S3 bucket policies
- S3 replication setup
- Logging and Monitoring
- S3 Storage Classes
- Data encryption at rest and in transit
## AWS Snowball
- It's a physical device to perform offline big data migration
- Highly-secure portable devices to *collect and process data at the edge, and migrate data into and out of AWS
- Helps migrate up to *Petabytes* of data

There are 2 types of snowball edge devices

| Device                            | Compute   | Memory | Storage (SSD) |
| --------------------------------- | --------- | ------ | ------------- |
| Snowball Edge *Storage* Optimized | 104 vCPUs | 416 GB | 210 TB        |
| Snowball Edge *Compute* Optimized | 104 vCPUs | 416 GB | 28 TB         |
*AWS Snowball:* offline devices to perform data migrations if it takes more than a week to transfer over the network, we use snowball devices
### What is edge computing?

- Process data while it's being created on an edge location
   - For example: a truck on the road, a ship on the sea, mining station underground, where these people don't have access to internet
- These locations may have limited internet and no access to computing power
- We order and set up *Snowball Edge Devices* to do edge computing
  - Snowball Edge compute optimized (*dedicated for this use case*) & storage optimized
Some use cases for edge computing: *preprocess data, machine learning, transcoding media*
## Snowball Edge Pricing: (*imp exam*)
We have to pay for everything except for data transfer IN to Amazon S3 is $0.00 per GB 

## AWS Storage Gateway
- *AWS Storage Gateway* allows us to bridge whatever happens on premises directly to the cloud so we can have a hybrid storage system for our organization
 ***
# Databases

- Storing data on disk (EFS, EBS, EC2 Instance Store, S3) can have it's limitations
- Sometimes, you want to store data in a database instead

