# Amazon S3
  - Amazon S3 is one of hte main building blocks of AWS
  - It's advertised as "infinitely scaling" storage
  - Many websites use Amazon S3 as a backbone
  - Many AWS services uses Amazon S3 as an integration as well

## S3 Use cases
  - Backup and storage
  - Disaster Recovery
  - Archive
  - Hybrid Cloud storage
  - Application Hosting
  - Media hosting
  - Data lakes and big data analytics
  - Software delivery
  - Static website

## Amazon S3 Overview - Buckets
  - Amazon S3 allows people to store objects (files) in "buckets" (directories)
  - Buckets must have a __globally unique name (across all regions all accounts)__
  - Buckets are defined at the region level
  - S3 looks like a global service but buckets are created in a region
  - Naming Convention:
    - No uppercase
    - No underscore
    - 3-63 characters long
    - Not an IP
    - Must start with lowercase letter or number

## Amazon S3 Overview - Objects
  - Objects (files) have a Key
  - The `key` is the __FULL__ path:
    - s3://my-bucket/`my_file.txt`
    - s3://my_bucket/`my_folder/another_folder/my_file.txt`
  - The key is composed of  a prefix + object name
    - prefix = `my_folder/another_folder/`
    - object name = `my_file.txt`
  - There's no concept of "directories" within buckets (although the UI will trick you to tink otherwise)
  - Just keys with very long names that contain slashes ("/")
  - Object values are the content of the body:
    - Max object size is 5TB (500GB)
    - If uploading more than 5GB, must use "multi-part upload"
  - Metadata (list of text key/value pairs - system or user metadata)
  - Tags (unicode key/value pair - up to 10) - useful for security/lifecycle
  - Version ID (if versioning is enabled)

# S3 Security
  - User based
    -  IAM Policies - which API calls should be allowed for a specific user from IAM console
  - Resource Based
    - Bucket Policies - bucket wide rules from the S3 console - allows  across account
    - Object Access Control List (ACL) - finer grain
    - Bucket Access Control List (ACL) - less common
  - Note: an IAM principal can access an S3 object if
    - the user IAM permissions allow it OR the resource policy ALLOWS it
    - AND there's no explicity DENY
  - Encryption: encrypt objects in Amazon S3 using encryption keys

## Example: Public Access - Use Bucket Policy
![Public Access Bucket Policy](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/public-access-bucket-policy.png)

## Example: User Access to S3 - IAM Permissions
![User Access to S3](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/user-access-to-s3-iam.png)

## Example: EC2 instance access - Use IAM Roles
![EC2 instance access](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/ec2-instance-iam-roles.png)

## Example: Cross-Account Access - Use Bucket Policy
![Cross-Account Access](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/cross-account-access.png)
 
## S3 Bucket Policies
  -  JSON based policies
    - Resources: buckets and objects
    - Actions:  Set of API to Allow  or Deny
    - Effect: Allow/Deny
    - Principal: The account or user to apply the policy to

  - Use S33 bucket for policy to:
    - Grant public access to the bucket
    - Force objects to be encrypted at upload
    - Grant access to another account (Cross Account)

## Bucket settings for Block Public Access
  - These settings were created to prevent company data leaks
  - If you know yourbucket should never be public, leave these on
  - Can be set at the account level

## Amazon S3 - Versioning
  - You can version your files in Amazon S3
  - It is enabled at the `bucket level`
  - Same key overwrite will increment the 'version': 1,2,3...
  - It is best practice to  version your buckets
    - Protect against unintended deletes (ability to restore a version)
    - Easy roll back to previous version
  - Notes:
    - Any file that is not versioned prior to enabling versioning will have version 'null'
    - Suspending versioning does not delete the previous versions

## Amazon S3 - Server Access Logging
  - For audit purposes, you may want to `log all access to S3 buckets`
  - Any request made to S3, from any account,  authorized or denied, will be logged into another S3 bucket
  - That data can be analyzed using data analysis tools
  - Very helpful to come down to the root cause of an issue, or audit usage, view suspicious patterns, etc...

## S3 - Replication Overview (CRR - cross region replication & SRR - same region replication)
  - `Must enable versioning` in source and destination
  - Cross Region Replication (CRR)
  - Same Region Replication (SRR)
  - Buckets can be in different accounts
  - Copying is asynchronous
  - Must give proper IAM permissions to S3
  - CRR - Use cases: compliance, lower latency access, replication across accounts
  - SRR - Use cases: log aggregation, live replication between production and test accounts

## S3 - Store Classes Overview
  - Amazon S3 Standard - General Purpose
  - Amazon S33 Standard-Infrequent Access (IA)
  - Amazon S3 One Zone-Infrequent Access
  - Amazon S3 Intelligent Tiering
  - Amazon Glacier
  - Amazon Glacier Deep Archive
  - Amazon S3 Reduced Redundancy Storage (deprecated)

### Durability and Availablity
  - Durability - how often you will lose a file:
    - High durability of objects across multiple AZ
    - If you store 10,000,000 objects within Amazon S3, you can on average expect to incur a loss of a single object once every 10,000 years
    - Same for all storage classes
  - Availability:
    - Measures how readily available a service is
    - S3 standard has 99.99% availability, which means it will not be available 53 minutes a year
    - Varies depending on storage class

### S3 Standard - General Purpose
  - 99.99% Availability
  - Used for frequently accessed data
  - Low latency and high throughput
  - Sustain 2 concurrent facility failures
  - Use Cases: Big Data analytics, mobile and gaming applications, content distribution

### S3 Standard - Infrequent Access (IA)
  - Sustainable for data that is less frequently access, but requires rapid access when needed
  - 99.99% availability
  - Lower cost compared to Amazon S3 Standard, but retrieval fee
  - Sustain 2 concurrent facility failures
  - Use cases: As a data store for disaster recovery, backups...

### S3 Intelligent Tiering
  - 99.99% availablity
  - Same low latency and high throughput performance of S3 Standard
  - `Cost-optimized by` automatically moving objects between two access tiers based on changing access patterns
    - Frequent access
    - Infrequent access
  - Resilient against events that impact an entire Availability Zone

### S3 One Zone - Infrequent Access (IA)
  - Same as IA but data is stored in a single AZ
  - 99.95% availablity
  - low latency and high throughput performance
  - lower cost compared to S3-IA (by 20%)
  - Use cases: Storing secondary backup copies of on-premise data, or storing data you can recreate

### Amazon Glacier and Glacier Deep Archive
  - Low cost object storage (in GB/month) meant for archiving/backup
  - Data is retained for the longer term (years)
  - Various retrieval options of time + fees for retrieval
  - `Amazon Glacier` - cheap:
    - expedited (1 to 5 minutes)
    - Standard (3 to 5 hours)
    - Bulk (5 to 12 hours)
  - Amazon Glacier Deep Archive - cheapest:
    - Standard (12 hours)
    - Bulk (48 hours)

### S3 - Moving between storage classes
  - You can transition objects between storage classes
  - For infrequent accessed object, move them to STANDARD_IA
  - For archive objects, you don't need in real-time, GLACIER or DEEP_ARCHIVE
  - Moving objects can be automated using a `lifecycle configuration`

## S3 Object Lock & Glacier Vault Lock
  - S3 Object Lock
    - Adopt a WORM (Write Once Read Many) model
    - Block an object versiond eletion for a specified amount of time
  - Glacier Vault Lock
    - Adrop a WORM (Write Once Read Many) model
    - Lock the policy for future edits (can no longer be changed)
    - Helpful for compliance and data retention

## Shared Responsibility Model
  - AWS
    - Infrastructure (global security, durability, availability, sustain concurrent loss of data in 2 facilities)
    - Configuration and vulnerability analysis
    - Compliance validation
  - Customer
    - S3 versioning
    - S3 Bucket policies
    - S3 Replication Setup
    - Logging and Monitoring
    - S3 Storage Classes
    - Data encryption at rest and in transit

## AWS Snow Family
  - Highly-secure, portable devices to `collect and process data at the edge` and `migrate data into and out of AWS`
  - Data Migration: Snowcone, Snowball Edge, Snowmobile
  - Edge Computing: Snowcone, Snowball Edge

### Data Migration with AWS Snow Family
  - Time to transfer data can take a long time over network
  - Challenges:
    - limited connectivity
    - limited bandwith
    - high network cost
    - shared bandwith (can't maximize the line)
    - connection stability

AWS Snow Family: offline devices to perform data migrations - if it takes more than a week to transfer over the network, use Snowball devices

### Diagrams
![Snow Diagrams](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/snow-diagrams.png)  

### Snowball Edge (for data transfers)
  - Physical data transport solution: move TBs or PBs of data in or out of AWS
  - Alternative to moving data over the network (and paying network fees)
  - Pay per data transfer job
  - Provide block storage and Amazon S3-compatible object storage

### Snowball Snowcone
  - Small,portable computing, anywhere, rugged and secure, withstands hard environments
  - light
  - device used for edge computing, storage, and data transfer
  - 8 TBs of usable storage
  - Use Snowcone where snowball does not fit (space contrained environment)
  - Must provie your own battery cables
  - Can be sent back to AWS offline, or connect it to internet and use AWS DataSync to send data

### AWS Snowmobile
  - Transfer exabytes ofdata 
  - Each snowmobile has 100 PB of capacity (use multiple in parallel)
  - High security
  - Better than Snowball if you transfer more than 10 PBs

### Snow Family - Usage Process
1. Request Snowball devices from the AWS console for delivery
2. Install the snowball client/AWS OpsHub on your servers
3. Connect the snowball to your servers and copy  file using the client
4. Ship back the device when you're done (goes to the right AWS facility)
5. Data will be loaded into an S3 bucket
6. Snowball is completely wiped

### What is Edge Computing
  - Process data while it's being created on an `edge location`
    - A truck on the road, ship on the sea, a mining station underground
  - These locations may have
    - Limited/no internet access
    - Limited/no easy access to computing power
  - We setup a Snowball Edge/Snowcone device to do edge computing
  - Use cases of Edge Computing:
    - Preprocess data
    - Machine learning at the edge
    - Transcoding media streams
  - Eventually (if need be) we can ship back to AWS (fro transferring data for example)

### Snow Family - Edge Computing
  - Snowcone (smaller)
  - Snowball Edge - Compute Optimized
  - Snowball Edge - Storage Optimized
  - All: Can run EC2 instances & AWS  Lambda functions (using AWS IoT Greengrass)
  - Long-term deployment options: 1 and 3 years discounted pricing

### AWS OpsHub
  - Historically, to use the Snow Family devices, you needed a CLI
  - AWS OpsHub - a software you can install on your computer to manage your Snow Family Device

## Storage Gateway Overview

### Hybrid Cloud for Storage
  - AWS is pushing for ”hybrid cloud”
    - Part of your infrastructure is on-premises 
    - Part of your infrastructure is on the cloud
  - This can be due to
    - Long cloud migrations
    - Security requirements
    - Compliance requirements 
    - IT strategy
  - S3 is a proprietary storage technology (unlike EFS / NFS), so how do you expose the S3 data on-premise?
  -  AWS Storage Gateway!

### AWS Storage Gateway
  - Bridge between on-premise data and cloud data in S3
  - Hybrid storage service to allow on- premises to seamlessly use the AWS Cloud
  - Use cases: disaster recovery, backup & restore, tiered storage
  - Types of Storage Gateway: 
    - File Gateway
    - Volume Gateway 
    - Tape Gateway
  - No need to know the types at the exam

Amazon S3 – Summary
  - Buckets vs Objects: global unique name, tied to a region
  - S3 security: IAM policy, S3 Bucket Policy (public access), S3 Encryption
  - S3 Websites: host a static website on Amazon S3
  - S3 Versioning: multiple versions for files, prevent accidental deletes
  - S3 Access Logs: log requests made within your S3 bucket
  - S3 Replication: same-region or cross-region, must enable versioning
  - S3 Storage Classes: Standard, IA, 1Z-IA, Intelligent, Glacier, Glacier Deep Archive   
  - S3 Lifecycle Rules: transition objects between classes
  - S3 GlacierVault Lock / S3 Object Lock:WORM (Write Once Read Many)
  - Snow Family: import data onto S3 through a physical device, edge computing
  - OpsHub: desktop application to manage Snow Family devices
  - Storage Gateway: hybrid solution to extend on-premises storage to S3  