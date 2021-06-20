#  Amazon EC2
  - One of the most popular of AWS' offering
  - Elastic Compute Cloud - Infrastructure as a Service
  - It main consists in the capability of:
    - Renting virtual mahcines (EC2)
    - Storing data on virtual drives (EBS)
    - Distributing load across machines (ELB)
    - Scaling the services using an auto-scaling group (ASG)
  - Knowing EC2 is fundamental to understand how the Cloud works


## EC2 Sizing and Configuration Options
  - Operating system (OS): Linux, Windows, Mac OS
  - How much computer power and cores (CPU)
  - How much random-access emmory (RAM)
  - How much storage space:
    -  Netwokr attached (EBS and EFS)
    - Hardware (EC2 instance store)
  - Network card : speed of the card, Public IP address
  - Firewall ruels: security group
  - Bootstrap script (configure at first launch): EC2 User Data

## EC2 User Data
  - It's possible to bootstrap our instance using an EC2 User Data script.
  - bootstrapping means lunaching command when a machine starts
  - That script is only run once at the instance first start
  - EC2 user data is used to automate boot tasks such as:
    - installing updates
    - installing software
    - donwloading common files from the internet
    - anything you can think of
  - The EC2 User Data Script run with the root user

## EC2 instance types - Overview
  - You can use different types of EC2 instance that are optimised for different use cases - (https://aws.amazon.com/ec2/instance-types/)
  - AWS has the following naming convention: m5.2xlarge
    m: instance class
    5: generation (AWS improves them over time)
    2xlarge: size within the instance class

## EC2 Instance Types - General Purpose
  - Great for diversity of workloads such as web servers or code repositories
  - Balance between:
    - Compute
    - Memory
    - Networking
  - In the course, we will be using the t2.micro which is a General Purpose EC2 isntance

### EC2 Instance Types - Compute Optomized
  - Great for computer-intensive tasks that require high performance processors:
    - Batch processing workloads
    - Media transcoding
    - High performance web servers
    - High performance computing (HPC)
    - Scientific modeling and machine learning
    - Dedicated gaming servers

## EC2 Instance Types - Memory Optpmized
  - Fast performance for workloads that process large data sets in memory
  - Use cases:
    - High performance, relation/non-relational databases
    - Distributed web scale cache  stores
    - In-memory databases optomized for BI (business inteliggence)
    - Application performing real-time processing of big unstructured data

## EC2 Instance Types - Storage Optimized
  - Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
  - Use cases:
    - High frequency online transaction processing (OLTP) systems
    - Relational and NoSQL databases
    - Cache for in-memory databases 
    - Data warehousing applications
    - Distributed file systems

<br><br>

# Introduction to Security Groups
  - Security Groups are the fundamental of netowrk security in AWS
  - They control how traffic is allowed into or out of our EC2 instances
  - Security groups only contain `allow` rules
  - Security groups rules can be reference by IP or by security group

## Security Groups Deeper Dive
  - Security groups are acting as a "firewall" on EC2 instances
  - They regulate:
    - Access to Ports
    - Authorised IP ranges - IPv4 and IPv6
    - Control of inbound network (from others to the instance)
    - Control of outbound network (from  the instance to others)

## Security Groups Good to Know
  - Can be attached to multiple instances
  - Locked down to a region /VPC combination
  - Does live"outside" the EC2 - if traffic is blocked the EC2 instance won't see it
  - It's good to maintain one separate security group for SSH access
  - If your application is not accessbile (time out), then it's a security group issue
  - If you application gives a "connection refused" error, then it's an application error or  it's not launched
  - All inbounce traffic is `blocked` by default
  - All outbound traffic is `authorized` by default
  - Security groups can reference other security groups inside of it. Think of an AD group having AD groups within it. Makes management a little easier so you don't have to go down to the "user" level aka IP address (in networking world)

## Classic Ports to know
  - 22 = SSH (secure shell) - log into a linux instance
  - 21 = FTP (file transfer protocol) - upload files into a file share
  - 22 = SFTP (secure file transfer protocol) - upload files using SSH
  - 80 = HTTP - access unsecured websites
  - 443 = HTTPS - access secured websites
  - 3389 = RDP (remote desktop protocol) - log into a Windows instance

EC2 instances can have many security groups
Security Groups can belong to many EC2 instances

## SSH Summary Table
![SSH Summary Table](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/ssh-terminal-diagram.png)

# How to SSH into your EC2 instance - Linux/Mac OSX
  - SSH is one of the most improtant function. It allows you to control a remote machine, all using the command line
  - we used `ec2-user` as the user when logging in via ssh
  - We attempted to ssh into our machine just normal but got denied, console output below:

  ```console
    (base) ~$ ssh ec2-user@52.87.212.147
    ec2-user@52.87.212.147: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
  ```
  
  - To ssh from terminal on macbook, needed to make sure we had the `.pem` file downloaded and that it had permissions `0400`. We attempted to login with the key pair file when it had permissions `0644` but we got the following error:
  
  ```console
    (base) ~/PycharmProjects/udemy-cloud-practitioner$ ssh -i configs/EC2Tutorial.pem ec2-user@52.87.212.147
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    @         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
    @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    Permissions 0644 for 'configs/EC2Tutorial.pem' are too open.
    It is required that your private key files are NOT accessible by others.
    This private key will be ignored.
    Load key "configs/EC2Tutorial.pem": bad permissions
    ec2-user@52.87.212.147: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
  ```

  - After updating the permissions on the `.pem` file to 0400, we were able to log in.

  ```console
  (base) ~/PycharmProjects/udemy-cloud-practitioner$ ls -al configs/
total 8
drwxr-xr-x   3 gustavoranz  staff    96 Jun 19 12:39 .
drwxr-xr-x  10 gustavoranz  staff   320 Jun 19 12:38 ..
-r--------   1 gustavoranz  staff  1704 Jun 19 12:39 EC2Tutorial.pem
(base) ~/PycharmProjects/udemy-cloud-practitioner$ ssh -i configs/EC2Tutorial.pem ec2-user@52.87.212.147
Last login: Sat Jun 19 16:42:14 2021 from c-73-212-233-102.hsd1.va.comcast.net

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
[ec2-user@ip-172-31-62-137 ~]$
```

# EC2 Instances Purchasing Options
  - On-Demand Instnces: short workload, predictable pricing
  - Reserved: (MINIMUM 1 year)
    - Reserved Instances: long workloads
    - Convertible Reserved Instances: long workloads with flexible instances
    - Scheduled Reserve Instances: example - every Thursday between 3 and 6 pm
  - Spot instances: short workloads, cheap, can lose instances (less reliable)
  - Dedicated Hosts: book an entire physical server, control instance placement

## EC2 On Demand
  - Pay for what you use:
    - Linux - billing per second, after the first minute
    - all other operating systems (ex. Windows) - billing per hour
  - Has the highest cost but no upfront payment
  - No long-term commitment
  - Recommended for `short-term` and  `un-interrupted workloads`, where you can't predict how the application will behave.

## EC2 Reserved Instances
  - Up to 75% discount compared to On-deman
  - Reservation period: 1 year = + discount | 3 years = +++ discount
  - Purchasing options: no upfront | partial upfront = + discount | All upfront = ++ discount
  - Reserve a specific instance type
  - Recommended for steady-state usage applications (think database)

  ### Convertible Reserved Instance
    - can change the EC2 instance type
    - up to 54% discount

  ### Scheduled Reserved Instances
    - launch within time window you reserve
    - when you require a fraction of day/week/month
    - still commitment over 1 to 3 years

##  EC2 Spot Instances
  - can get a discount of up to 90% compared to On-demand
  - Instances that you can "lose" at any point of time if your max price is less tahn the current spot price
  - The MOST cost-efficient isntances in AWS

  <br>

  - Useful for workloads that are resilient to failure
    - batch jobs
    - data analysis
    - image processing
    - any distributed workloads
    - workloads with a flexible start and end time
  
    <br>
    
  - __Not suitable for critical jobs or databases__