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
  - Controls the EBS behavior when an EC2 instance terminates
    - By default the root EBS volume is deleted (attribute enabled)
    - By default, any other  attached EBS volume is __not__ deleted (attribute disabled)
  - This can be controlled by the AWS console/AWS CLI
  - __Use case: preserve root volume when instance is terminated__

## EBS Snapshots
  - Make a backup (snapshot) of your EBS volume at a point in time
  - Not necessary to detach volume to do snapshot, but recommended
  - Can copy snaoshots across AZ or Region
  
![EBS Snapshot](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/ebs-snapshot.png)

## AMI Overview
  - AMI = Amazon Machine Image
  - AMI are __customization__ of an EC2 instance
    - You add your own software, configurations, operating system, monitoring...
    - Faster boot/ configuration time because all your software is pre-packaged
  - AMI are built of a __specific region__ (and can be copied across regions)
  - You can launch EC2 instances from:
    - A Public AMI: AWS provided
    - Your own AMI: You make and maintain them yourself
    - An AWS Marketplace AMI: an AMI someone else made (and potentially sells)
  
## AMI Process (from an EC2 instance)
  - Start an EC2 instance and customize it
  - Stop the instance (for data integrity)
  - Build an AMI - this will also create EBS snapshots
  - Launch instances from other AMIs

![Custom AMI](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/custom-ami.png)


## EC2 Image Builder
  - Used to automate the creation of Virtual Machines or container images
  - => Automate the creation, maintain, validate and test EC2 AMIs
  - Can be run on a schedule (weekly, whenever packages are updated, etc...)
  - Free service (only pay for the underlying resources)
![EC2 Image Builder](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/ec2-image-builder.png)


## EC2 Instance Store
  - EBS volumes are __network drives__ with good but "limited" performance
  - __if you need a high-performance hardware disk, use EC2 Instance Store__
  <br>
  - Better I/O performance
  - EC2 Instance Store lose their storage if they're stopped (ephemeral)
  - Not good for as a durable long-term place to store data
  - Good buffer/cache/scratch data/temporary content
  - Risk of data loss if hardware fails
  - Backups and Replication are __your responsibility__

## EFS - Elastic File System
  -  Managed NFS (network file system) that __can be mounted on 100s of EC2__
  - EFS works with __Limux EC2__ instances in __multi-AZ__
  - Highly available, scalable, expensive (3x gp2), pay per use, no capacity planning

## EBS vs EFS
![EBS vs EFS](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/ebs-vs-efs.png)
  - EBS can only be attached to ONE instance in ONE AZ
  - EBS volumes are bound to ONE availability zone
  - If we wanted to move the EBS volume over to another AZ, we would create an EBS Snapshot and then restore that snapshot into the new availability zone
    - This is a __copy__ NOT an __in-sync__ replica
  
  <br>
  
  - EFS is a network file system which means that whatever is on the EFS drive is _shared_ by everything that is mounted to it.
  - Say we have many instances on AZ1 and many instances on AZ2, at the same time all the instances can mount the EFS mount and they will ALL see the same files. That's what makes it a "shared file system"

## EFS Infrequent Access (EFS-IA)
  - __Storage class__ that  is cost-optomized for files not accessed every day
  - Up to 92% lower cost compared to EFS Standard
  - EFS will automatically move your files to EFS-IA based on the last time they were accessed
  - Enable EFS-IA with a Lifecycle Policy
  - Example: move files that are not accessed for 60 days to EFS-IA
  - Transparent to the applications accessing EFS

## Shared Responsibility Model of EC2 Storage
  - AWS
    - Infrastructure
    - Replication for data for EBS volumes and EFS drives
    - Replacing faulty hardware
    - Ensuring their employees cannot access your data
  
  - User
    - Setting up backup/snapshot procedures
    - Setting up data encryption
    - Responsibility of any data on the drives
    - Understanding the risk of using EC2 Instance Store

## Amazon FSx for Windows File Server
  - A fully managed, highly reliable, and scalable __Windows Native__ shared file system
  - Built on __Windows File Server__
  - Supports __SMB protocol__ and Windows NTFS
  - Integrated with Microsoft Active Directory
  - Can be accessed from AWS or your on-premise infrastructure

## Amazon FSx for Lustre
  -  A fully managed, high-performance, scalable file storage for __High Performance Computing (HPC)__
  - The name Lustre is derived from "Linux" and "Cluster"
  - Machine learning, Analytics, Video Processing, Financial Modeling...
  - Scales up to 100s GB/s, millions of IOPS, sub-ms latencies

## EC2 Instance Storage - Sumarry
  - EBS Volumes:
    - network drives attached to one  EC2 instance at a time
    - Mapped to an Availability Zones
    - Can use EBS Snapshots for backups/transferring EBS volumes across AZ
  - AMI: create ready-to-use EC2 instances with our customizations
  - EC2 Image Builder: Automatically, build, test and distribute AMIs
  - EC2 Instance Store: 
    - High performance hardware disk attached to our EC2 instance
    - Lost if our instance is stopped/terminated
  - EFS: network file system, can be attached to 100s of instances in a region
  - EFS-IA: cost-optomized storage class for infrequent accessed files