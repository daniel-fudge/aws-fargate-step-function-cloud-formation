# aws-fargate-step-function-cloud-formation
Small repo that creates an AWS Step Function to call Fargate tasks with cloud formation.

This repo follows from this [repo](https://github.com/daniel-fudge/aws-fargate-step-function-demo) 
which also deployed an AWS Step Function that calls Fargate tasks. However that repo 
performed this with AWS CLI commands. This repo creates the same infrastructure but with 
the AWS Cloud Formation (CF) Infrastrucutre as Code (IaC).

We'll actually build the components with individual components first to validate each 
piece and then we'll bring it all together in a single CF file.

1. Setup the environment
1. Fargate ECS Task
1. Step Function
1. Bring it all together

## 1. Setup the Environment
### Configure the AWS Console
Before completing the following CLI command, you need to install the AWS CLI and configure 
it for the account, role and region you wish to use. I use the `aws configure sso` command.

### First set some environment variables
```shell
export BUCKET=[ENTER YOUR BUCKET NAME HERE]
export AWS_PROFILE=[ENTER YOUR CLI PROFILE NAME HERE]
export AWS_PAGER=""
export AWS_REGION=us-east-1
export CIDR_VPC=10.0.0.0/16
export CIDR_SUBNET1=10.0.0.0/24
export CIDR_SUBNET2=10.0.1.0/24
```


## 1. Fargate ECS Task Stack
Create the stack and wait for it to be completed.
```shell
aws cloudformation create-stack --stack-name task --template-body file://task.yml \
--parameters ParameterKey=Bucket,ParameterValue=${BUCKET} \
ParameterKey=CidrVpc,ParameterValue=${CIDR_VPC} \
ParameterKey=CidrSubnet1,ParameterValue=${CIDR_SUBNET1} \
ParameterKey=CidrSubnet2,ParameterValue=${CIDR_SUBNET2}
aws cloudformation wait stack-create-complete --stack-name task
```
To delete the stack and wait for it to be deleted:
```shell
aws cloudformation delete-stack --stack-name task
aws cloudformation wait stack-delete-complete --stack-name task
```


## 2. IAM Roles

## 3. ECR Image

## 4. Fargate ECS Task

## 5. Step Function

## 6. Bring it all together

## 7. References
 - [CLI Repo Version](https://github.com/daniel-fudge/aws-fargate-step-function-demo)    
 - [Cloud Formation Example Repo](https://github.com/nathanpeck/aws-cloudformation-fargate)    


 https://docs.aws.amazon.com/codebuild/latest/userguide/cloudformation-vpc-template.html    

