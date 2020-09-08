## 0001. Record architecture decisions

Date: 2018-08-08

# Status

Accepted

# Context

We need to record the architectural decisions made on this project.

# Decision

We will use Architecture Decision Records, as described by Michael Nygard in this article: http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions

# Consequences

See Michael Nygard's article, linked above. For a lightweight ADR toolset, see Nat Pryce's _adr-tools_ at https://github.com/npryce/adr-tools.


## 0002. Keep it Simple

Date: 2020-08-27

# Status

Accepted

# Context

We need to keep the solution quick and simple

# Decision

We will keep the solution simple and easy to use and reduce complexity.

# Consequences

As ideal as it would be to use CI/CD pipelines, the concept of the task is to be able to load from any git repository and run deploy command to quickly demonstrate how to quickly deploy app to cloud.


## 0003. AWS Selected Cloud Platform

Date: 2020-08-27

# Status

Accepted

# Context

There are three major cloud platforms to deploy the platform on.

# Decision

We decided to use AWS cloud as the developer is most familiar with this platform, making development quick and simple.

# Consequences

The assessment team may want to see another cloud platform demonstrated.

## 0004. Solution developed using Ansible Script

Date: 2020-08-27

# Status

Accepted

# Context

There are many different languages and solutions to choose to build a solution and one assessment objective is to be able to just be able to clone from git and run the application.

# Decision

I decided to use ansible bash scripting as its native on both Linux and MacOS platforms.
It allows the use of native ansible commands to create the solution, negating the need for extra installations.

Ansible also integratrates with CI/CD pipelines such as circleci and Jenkins, meaning you can run the playbook from a CI/CD pipeline as required.

# Consequences

More time required to de


## 0005. Virtual Network Configuration

Date: 2020-08-27

# Status

Accepted

# Context

There are many few different ways to configure network zones within AWS to provide different types of solutions. ie. Separate WEB, APP and DB Tiers.

# Decision

Two network zones are configured to host the application. 
Public WebDMZ zone which is accessible to the outside world via port 80 (or preferred port depending on configuration setting in variable files).
Private RDS zone which cannot connect to servers outside of VPC.  Servers in the public DMZ can access RDS zone via default postgressql port 5432 (or can specify another port in variable file).

# Consequences

Longer time to setup and develop

## 0006. ECS Instance Type

# Context

There are two different ECS laucnch configurations, ECS2 and Fargate

# Decision

We are going to use the EC2 ECS instances, as its cheaper to use for for such instances of web server application that run continuously.

# Consequences

Fargate autoscales easier, has lower maintenance than EC2 and AWS manage the service, reducing work.

## 0007. ECS Instance Size

Date: 2020-09-01

# Status

Accepted

# Context

There are many different ECS instance sizes t2.medium, t2.micro, etc

# Decision

We are going to use t2.micro as its part of the aws free tier and gives 750 hours of computing for the month.  At this point in time capacity is not crucial in this test scenario.

# Consequences

t2.micro not a great option for busy applciation, that is handling multiple requests.  If this become an issue ESC Fargate should be able to handle the autoscaling for us.

## 0008. Build local docker image

Date: 2020-09-01

# Status

Accepted

# Context

The docker image can be built different ways, locally, via pipeline, or remotely

# Decision

The easiest and quickest way to perform the requested task is to build the docker image locally.  It would be great to do it remotely via docker-compose file but as of current time, the build directive is not supported in docker-compose files in AWS.

# Consequences

Not an elegant solution and requires local resource to have Docker installed and accesible by user running request.
