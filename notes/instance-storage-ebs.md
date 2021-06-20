# EC2 Instance Storage

## What's an EBS Volume
  - an EBS (Elastic Block Store) Volume is a _network_ drive you can attached to your instances while they run
  - It allows your instances to persist data, even after their termination
  - _They can only be mounted to one instance at a time__ (at the CCP level)
    - CCP - Certified Cloud Practioner - one EBS can only be mounted to one EC2 instance 
    - Associate Level (Solutions Architect, Developer, SysOps) - "multi-attach" feature for some EBS
  - They are bound to _a specific availability zone_

  <br>
  - Analogy: Think of them as a "network USB stick"
  
# EBS Volume
  - It's a network drive (i.e. not a physical drive)
    - It uses the network to communicate the instance, which means there might be a bit of latency
    - It can be detached from an EC2 instance and attached to another one quickly
  - It's locked to an Availability Zone (AZ)
    - An EBS Volume in us-east-1a cannot be attached to us-east-1b
    - To move a volume across, you first need to snapshot It
  - Have a provisioned capacity (size in GBs, and IOPS)
    - You get billed for all the provisioned capacity
    - You can increase the capacity of the driver over time

## EBS Volume Example
  - You can multiple EBS volumes linked to the same instance
  - You can leave EBS volumes unattached
![EBS Volume Example](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/ebs-volume-example.png)

## EBS - Delete on Termination Attribute
![EBS Delete on Termination](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/ebs-delete-on-termination.png)
  - Controls teh EBS behavior when an EC2 instance terminates
