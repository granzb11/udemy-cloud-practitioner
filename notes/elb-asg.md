# Elastic Load Balancing (ELB) & Auto Scaling Groups (ASG)

## Scalability and High Availability
  - Scalability means that an application/system can handle greater loads by adapting
  - There are 2 kind of scalability:
    - Vertical Scalability
    - Horizontal Scalability (= elasticity)
  - __Scalability is linked but different to High Availability__
  <br>

  - Let's deep drive into the distinction, using a call center as an example

## Vertical Scalability
  - Vertical Scalability means increasing the size of the instance
  - Example is having a junior operator working in the  call center and then you hire a senior operator who can handle more calls than the  junior operator. This is vertical scalability
  - In AWS for example, your application runs on a t2.micro
  - Scaling that application vertically means running it on a t2.large
  - Vertical scalability is a very common for non distributed system, such as a database
  - There's usually a limit to how much you can vertically scale (hardware limit)

## Horizontal Scalability
  - Horizontal scalability means increasing the number of instances/systems for your application
  - In the same of the call center is that you instead hire 5 more junior operators to handle calls
  - Horizontal scaling implies `distributed systems`
  - This is very common for web applications/modern applications
  - It's easy to horizontally scale thanks to the cloud offerings such as Amazon EC2

## High Availability
  - High availability usually goes hand in hand with horizontal scaling
  - High availablity means running your application/system in at least `2 Availability Zones`
  - Call center example of this would be running a call center in New York and another one in San Francisco. If one of the call centers is down, we would re-route calls to San Francisco
  - The goal of high avaiability is to survive a data center loss (disaster)

## High Availability and Scalability for EC2
  - Vertical Scaling: Increate instance size (= scale up/down)
    - From: t2.nano 
    - To: u-12tb1.metal
  - Horizontal Scaling: Increase number of instances (= scale out/in)
    - Auto Scaling Group
    - Load Balancer
  -  High Availability: Run instances for the same application across multi AZ
    - Auto Scaling Group multi AZ
    - Load Balancer multi AZ

## Scalablity vs Elasticity (vs Agility)
  - Scalability: ability to accommodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale out)
  - Elasticity: Once a system is scalable, elasticity means that there will be some "auto-scaling" so that the system can scale based on the load. This is "cloud-friends": pay-per-use, match demand, optimize costs
  - Agility: (not related to scalability - distractor) new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes.

## What is load balancing?
  - Load balancers are servers that forward internet traffic to multiple servers (EC2 instances) downstream
  ![Load Balancer](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/load-balancer.png)

## Why use a load balancer?
  - Spread load across multuple downstream instances
  - Expose a single point of access (DNS) to your application
  - Seamlessly handle failures of downstream instances
  - Do regular health checks to your instances
  - Provide SSL termination (HTTPS) for your websites
  - High availability across zones

### Why use an Elastic Load Balancer
  - An ELB (Elastic Load Balancer) is a `managed load balancer`
    - AWS guarantees that it will be working
    - AWS takes care of the upgrades, maintenance, high  availability
    - AWS provides only a few configuration knobs
  - It costs less to setup your own load balancer but it will be a lot more effort on your end (maintenance, integrations)
  - 3 kinds of load balancers offered by AWS:
    - Application Load Balancer (HTTP/HTTPS only) - layer 7
    - Network Load Balancer (ultra-high performance, allows for TCP) - Layer 4
    - Classic Load Balancer (slowly retiring) - Layer 4 & 7

## What's an Auto Scaling Group?
  - In real-life, the lod on your websites and application can change
  - In the cloud, you can create and get rid of servers very quickly
  - The goal of an Auto Scaling Group (ASG) is to:
    - Scale out (add EC2 instances) to match an increased load
    - Scale in (remove EC2 instances) to match decreased load
    - Ensure we have a minimum and maximum number of machines running
    - Automatically register new instances to a load balancer
    - Replace unhealthy instances
  - Cost Savings: only run at an optimal capcity (principle of the cloud)

## Auto Scaling Group in AWS
![Auto Scaling Group](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/auto-scaling-group.png)

## Auto Scaling Group in AWS With Load Balancer
![Auto Scaling Group With Load Balancer](https://github.com/granzb11/udemy-cloud-practitioner/blob/main/images/auto-scaling-group-with-load-balancer.png)
