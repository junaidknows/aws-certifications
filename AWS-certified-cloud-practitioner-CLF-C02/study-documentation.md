This file contains my study notes for the *AWS Certified Cloud Practitioner CLF-C02* course. I'll document key concepts, practical insights, and important takeaways as I progress through the course.

*Course source:* 
[AWS Certified Cloud Practitioner CLF-C02](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/?couponCode=25BBPMXACCAGE1)
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

