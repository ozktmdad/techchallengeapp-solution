# 0001. Record architecture decisions

Date: 2018-08-08

## Status

Accepted

## Context

We need to record the architectural decisions made on this project.

## Decision

We will use Architecture Decision Records, as described by Michael Nygard in this article: http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions

## Consequences

See Michael Nygard's article, linked above. For a lightweight ADR toolset, see Nat Pryce's _adr-tools_ at https://github.com/npryce/adr-tools.


# 0002. Keep it Simple

Date: 2020-08-27

## Status

Accepted

## Context

We need to keep the solution quick and simple

## Decision

We will keep the solution simple and easy to use and reduce complexity.

## Consequences

As ideal as it would be to use CI/CD pipelines, the concept of the task is to be able to load from any git repository and run deploy command to quickly demonstrate how to quickly deploy app to cloud.


# 0003. AWS Selected Cloud Platform

Date: 2020-08-27

## Status

Accepted

## Context

There are three major cloud platforms to deploy the platform on.

## Decision

We decided to use AWS cloud as the developer is most familiar with this platform, making development quick and simple.

## Consequences

The assessment team may want to see another cloud platform demonstrated.

# 0004. Solution developed using BASH Script

Date: 2020-08-27

## Status

Accepted

## Context

There are many different languages and solutions to choose to build a solution and one assessment objective is to be able to just be able to clone from git and run the application.

## Decision

I decided to use bash scripting as its native on both Linux and MacOS platforms.
It allows the use of native commands and the least amount of additional libraries, language versions to make work.

## Consequences

BASH scripts are not natively supported on Windows and requires extra tools like CYGWIN


# 0005. Virtual Network Configuration

Date: 2020-08-27

## Status

Accepted

## Context

There are many few different ways to configure network zones within AWS to provide different types of solutions. ie. Separate WEB, APP and DB Tiers.

## Decision

I to use a single network zone in the interest of simplicity and get the application working and running quickly.

## Consequences

Having both the app and db in the same zone is poor from a secutiy point of view.

# 0006. ECS Instance Type

## Context

There are two different ECS laucnch configurations, ECS2 and Fargate

## Decision

We are going to use the Fargate ECS launch type, due to this task being a short start and stop type project.  It is more expensive to have a continuously running image but cheaper for testing and project work.

Another advantage of Fargate is it autoscales easier, has lower maintenance than EC2 and AWS manage the service, reducing work.

## Consequences

Fargate is more expensive than EC2 for continuously running instances of an application.  ie. a webserver or web application which is what we are running in this test would be cheaper to run in EC2 but as this is a test, I'm cheap and don't want to pay for continuously running instances.


# 0007. ECS Instance Size

Date: 2020-09-01

## Status

Accepted

## Context

There are many different ECS instance sizes t2.medium, t2.micro, etc

## Decision

We are going to use t2.micro as its part of the aws free tier and gives 750 hours of computing for the month.  At this point in time capacity is not crucial in this test scenario.

## Consequences

t2.micro not a great option for busy applciation, that is handling multiple requests.  If this become an issue ESC Fargate should be able to handle the autoscaling for us.

# 0008. Build local docker image

Date: 2020-09-01

## Status

Accepted

## Context

The docker image can be built different ways, locally, via pipeline, or remotely

## Decision

The easiest and quickest way to perform the requested task is to build the docker image locally.  It would be great to do it remotely via docker-compose file but as of current time, the build directive is not supported in docker-compose files in AWS.

## Consequences

Not an elegant solution and requires local resource to have Docker installed and accesible by user running request.

