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

##