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
* In AWSyou apply the __least privilege principle__: don't give more permissions than a user needs
* Example JSON Policy:
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