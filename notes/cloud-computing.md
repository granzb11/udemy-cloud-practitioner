## Types of Cloud Computing

### Infrastructure as a Service (IaaS)
  * Provide building blocks for cloud IT
  * Provides networking, computers, data storage space
  * Highest level of flexibility
  * Easy parallel with traditional on-premises IT
  
Examples:
  * Amazon EC2 (on AWS)
  * GCP, Azure, Rackspace, Digital Ocean, Linode
  
> This is pretty much you building your own full application. With this support and maintainability falls back to the company.

<br>

### Platform as a Service (PaaS)
  * Removes the need for your organization to manage the underlying infrastructure
  * Focus on the deployment and management of your applications
  
Examples:
  * Elastic Beanstalk (on AWS)
  * Heroku, Google App Enginer (GCP), Windows Azure (Microsoft)
  
> An example of this would be the internal Control-M or DBT by Fishtown tools we have at USAA. The underlying infrastructure and code is given to us by the vendor but we must deploy the new updates ourselves.

<br>

### Software as a Service (SaaS)
  * Completed product that is run and managed by the service provider.
  
Examples: 
  * Many AWS services (ex: Rekognition for Machine Learning)
    
> I don't believe at USAA we have many SaaS applications, we try to bring in as much of these tools as we can internally. 
> I believe an example of SaaS is Slack.

<br><br>

## Comparing On-prem vs Cloud offerings

### Who manages what components

:white_check_mark: - Managed by you<br/>
:x: - Managed by others

| Components      | On-prem  | IaaS   | PaaS    | SaaS    |
| --------------- | -------- | ------ | ------- | ------- | 
| Applications    | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x: |
| Data            | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x: |
| Runtime         | :white_check_mark: | :white_check_mark: | :x: | :x: |
| Middleware      | :white_check_mark: | :white_check_mark: | :x: | :x: |
| O/S             | :white_check_mark: | :white_check_mark: | :x: | :x: |
| Virtualization  | :white_check_mark: | :x: | :x: | :x: |
| Servers         | :white_check_mark: | :x: | :x: | :x: |
| Storage         | :white_check_mark: | :x: | :x: | :x: |
| Networking      | :white_check_mark: | :x: | :x: | :x: |

<br><br>
## Pricing of the Cloud 
* AWS has 3 pricing fundamentals, following the pay-as-you-go pricing model.
* Computer:
  * Pay for compute time
* Storage:
  * Pay for data stored in the cloud
* Data transfer OUT of the Cloud:
  * Data transfer IN is free
* Solves the expensive issue of traditional IT

<br><br>
## How to choose an AWS Region?
If you need to launch a new application, where should you do it?
* __Compliance__ with data governance and legal requirements: data never leaves a region without your explicit permission
* __Proximity__ to customers: reduced latency
* __Available services__ within a Region: new services and new features aren't available in every Region
* __Pricing__ varies region to region and is transparent in the service pricing page