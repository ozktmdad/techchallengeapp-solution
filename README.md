## techchallengeapp-solution

> The solution to the techchallengeapp for DevOps engineer position at Servian

## Design

Solution is deployed in AWS VPC, across two separate a public DMZ zone available to the public on port 80 (default) and a private AWS RDS zone, which is only accessible from the WebDMZ zone only via the database port 5432 (default). Both the DMZ and RDS zones are spread accross three AWS availabilty zones.  

The PostgresSQL database is configured as multi-az for high availbiltiy, in the private RDS zone.

The application is deployed as multiple docker containers using AWS ECS service in the DMZ zone, behind a load balancer, and accessible publically on port 80 (default).

TODO: Load Balancer 

High Level Design diagram goes here.

## Prerequisites

# Plaform Prequistes
A *nix based system such as Linux or macos

# Software Prerequsites
ansible =~ 2.9.13
aws-cli =~ 2.0.44
ecs-cli =~ 1.20.0

# AWS Account Prerequiste 
Have configured AWS aws_access_key_id and secret access key IAM access abitiy to create, VPC, EC2, RDS and ECS instances.  (If you don't know how to do this you probably shouldn't be assessing me)

Please setup AWS access key and secretkey
Set pager in .aws/config in ecs-cli to
set cli_pager= 

Please refer to the following AWS documents for installation and configuration of AWS tools
https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_installation.html
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_Configuration.html

## Clone
- Clone this repo to your local machine using 
git clone https://github.com/ozktmdad/techchallengeapp-solution.git

## Setup

# Configure password vault

- Create vault password similar to ssh key to encrypt your usernames and passwords in playbook
```shell
$ echo "myvaultkey" > ~/techchallenge.vault
```
- Create three encrypted passwords using ansible-vault and techchallenge vault
1. aws_access_key_id
2. aws_secret_access_key
3. Database Password
```shell
$ ansible-vault encrypt_string "AZRXC5HHHBYVAKDAFJ4" --vault-password-file ~/techchallenge.vault
!vault |
          $ANSIBLE_VAULT;1.1;AES256
          38643064656331346431393332366133306439663532626131613532646138376165306431633937
          3330646664333730346462383262313631376664643366620a666231326637343830306532303531
          65393966616132373234323739616338313837316162343565346562316138323338336234353062
          3066376364383034310a643863623038353765316666393065373266386438643938333061313331
          63376330373861323537303737343134623962376663366262653235343366386630
Encryption successful
$ ansible-vault encrypt_string "ajdfkakfak4r4r4rnkafa6767jfafk" --vault-password-file ~/techchallenge.vault
!vault |
          $ANSIBLE_VAULT;1.1;AES256
          39666536353561636437613131626236343864343064666538363964656662313534373761366461
          3639663762646538373332323439643261356232366131650a376632613636643665313737636162
          63323961306437346532636134383761313931663830303736663362373836646165313736616361
          6633616337613930650a333062653136636437346236653232303361336166383232373831356662
          66303661376562623136313465623765643938346431386564656335386562613365
Encryption successful
 $ ansible-vault encrypt_string "CHANGEME" --vault-password-file ~/techchallenge.vault
!vault |
          $ANSIBLE_VAULT;1.1;AES256
          38303834643964623334393462363663323630383463353961666531323763316134333661663836
          6436613231613736366331376562313934636165323064620a326536633438663436346633626236
          30666134303933623334343931343465376666323962306536323065646536383339393538323664
          6665386565313232360a356462306165313937366430393966346637653361643766383232353538
          3662
Encryption successful
```
# Update encrypted passwords in the app

Open file group_vars/project.techchallengeapp.yml and update variables:
- DbPassword
- aws_access_key
- aws_secret_key

# Update solution variables as desired:

Open file group_vars/project.techchallengeapp.yml and update variables:
- DbUser  (The database user name)
- DbName  (Name of the Database)
- DbPort  (PostgresSQL default: 5432)
- ListenHost (The hosts which can use the applicaton)
- LIstenPort (The port the application runs on)
- external_port (The port users will use to access the application)
- aws_region (The AWS region to deploy the solution)

## Usage

Run ansible playbook to deploy the solution:
```shell
$ ansible-playbook -i hosts.inventory roles/techchallengeapp/tasks/main.yml --vault-password-file ~/techchallenge.vault
```

## Cleanup
Future Release feature

## TODO
- Add container instances to Load Balancer
- Write a cleanup resource playbook