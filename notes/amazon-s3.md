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
 