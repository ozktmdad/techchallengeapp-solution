## Prerequisites
AWS account with IAM access to RDS and ECS
AmazonEC2ContainerServiceforEC2Role
AWS access key and secretkey
aws cli https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
set cli_pager= in .aws/config
requires jq
Have installed ECS CLI, for installatin instructions please refer to:
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_installation.html

and configured AWS CLI configuration
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_Configuration.html
ecs-cli configure --cluster tech_challenge --default-launch-type FARGATE  --region us-east-1 --config-name servian

ECS user with correct permissions

## Setup
Install AWS
Clone repo
Configure config file
** Please ensure you update the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY variables
*** with your aws access key and secret key
Run deploy.sh

## Cleanup

Run cleanup.sh to remove all created resources

## Features
- ERRO[0003] Error running tasks                           error="InvalidParameterException: No Container Instances were found in your cluster." task definition=0xc000444210
FATA[0003] InvalidParameterException: No Container Instances were found in your cluster. 

If you see thiserror message don't panic everything still works it only happens because a EC2 hasn't been deployed in the cluster yet.  Application still works as per design.

- FATA[0001] Error executing 'up': A CloudFormation stack already exists for the cluster 'techchallengeapp-cluster'. Please specify '--force' to clean up your existing resources 

Your going to see this error if you are rerunning the script, the second time and its going to try and recreate all of the resorces for cloud formation again.  Doesn't effect the final result.

