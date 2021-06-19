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
![image info](/Users/gustavoranz/PycharmProjects/udemy-cloud-practitioner/images/ssh-terminal-diagram.png)