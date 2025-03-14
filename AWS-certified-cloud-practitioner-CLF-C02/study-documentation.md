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
