# IAM - Identity and Access Management

## IAM: Users & Groups
* IAM = Identity and Access Management, it is a __Global__ Service, this is very important to note.
* root account created by default, shouldn't be used or shared
* Users are people within your organization, and can be grouped
* Groups can only contain users, NOT other groups
* Users don't have to belong to a group, and a user can belong to multiple groups

## IAM: Permissions
* Users or Groups can be assigned JSON documents called Policies
* These policies define the __permissions__ of the users
* In AWS you apply the __least privilege principle__: don't give more permissions than a user needs
<details>
  <summary>Example JSON Policy:</summary>

```json
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Effect":"Allow",
      "Action":"ec2:Describe*",
      "Resource":"*"
    },
    {
      "Effect":"Allow",
      "Action":"elasticloadbalancing:Describe*",
      "Resource":"*"
    },
    {
      "Effect":"Allow",
      "Action":[
        "cloudwatch:ListMetrics",
        "cloudwatch:GetMetricStatistics",
        "cloudwatch:Describe*"
      ],
      "Resource":"*"
    }
  ]
}
```
</details>

## IAM Policies Inheritance
* Inline policy - policy that is solely attached to a user

## IAM Policies Structure
* Consists of
  * Version: policy language version (always include) 
  * Id: an identifier for the policy (optional)
  * Statement: one or more individual Statements (required)
Statements consists of
  * Sid: an identifier for the statement(optional)
  * Effect: whether the statement allows or denies access (Allow, Deny)
  * Principal: account/user/role to which this policy applied to
  * Action: list of actions this policy allows or denies
  * Resource: list of resources to which the actions applied to
  * Condition: conditions for when this policy is in effect (optional)
  
<details>
  <summary>* Example JSON</summary>
```json
{
  "Version":"2012-10-17",
  "Id":"S3-Account-Permissions",
  "Statement":[
    {
      "Sid":"1",
      "Effect":"Allow",
      "Principal":{
        "AWS":[
          "arn:aws:iam:123455678.root"
        ]
      },
      "Action":[
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource":[
        "arn:aws:s3:::mybucket/*"
      ]
    }
  ]
}
```
</details>  