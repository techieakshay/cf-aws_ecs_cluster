# AWS CloudFormation - ECS Cluster Deployment

This CloudFormation template creates an **Amazon ECS Cluster** with the following components:
- **ECS Cluster**: Hosts your containerized applications.
- **EC2 Instances**: Part of the ECS cluster, provisioned using Launch Configuration.
- **Security Group**: Secures access to the ECS instances.
- **Application Load Balancer (ALB)**: Distributes incoming traffic across ECS tasks.
- **Target Group**: Links the ALB to the ECS service.
- **Listener**: Forwards incoming traffic to the target group based on port/protocol settings.

## Features
- **Auto-Scaling EC2 instances**: The ECS cluster uses Auto Scaling for instance management.
- **Load Balancing**: Automatically distributes incoming traffic to ECS tasks.
- **Security Groups**: Configures security to allow access only from trusted sources.
- **Elastic Load Balancer Listener**: Forwards HTTP/HTTPS requests to the appropriate target group.

## Architecture
The stack consists of:
1. **ECS Cluster**: An empty ECS cluster that can run Docker containers.
2. **Auto Scaling Group**: Manages the number of EC2 instances in the ECS cluster.
3. **Load Balancer**: Balances traffic between ECS tasks.
4. **Security Group**: Allows access only to the necessary ports.
5. **Listener and Target Group**: Forwards traffic from the Load Balancer to ECS.

## Prerequisites
- AWS CLI or access to AWS Console.
- IAM permissions to create ECS, EC2, ALB, and related resources.
- Optional: Prebuilt Docker container image hosted in Amazon ECR or DockerHub.

## Deployment Instructions

### 1. Deploy the CloudFormation Stack

#### Using AWS Console
1. Navigate to the [AWS CloudFormation Console](https://console.aws.amazon.com/cloudformation/).
2. Click on **Create Stack** and choose **With new resources (standard)**.
3. Upload the CloudFormation template (e.g., `ecs-cluster.yml`) or provide the template URL.
4. Provide the necessary parameters if you want to override.
5. Click **Next**, configure stack options as needed, and proceed to **Create Stack**.

#### Using AWS CLI
You can also create the stack using the AWS CLI:
```bash

aws cloudformation create-stack --stack-name appecscluster --template-body file://cftemplate.json --capabilities CAPABILITY_NAMED_IAM --profile  my-profile 

- If you want to override the parameters from commandline, use below syntax
aws cloudformation create-stack --stack-name appecscluster  --parameters ParameterKey=ClusterName,ParameterValue=MyECSCluster \
               ParameterKey=InstanceType,ParameterValue=t2.micro \
               ParameterKey=KeyName,ParameterValue=MyKeyPair --template-body file://cftemplate.json --capabilities CAPABILITY_NAMED_IAM --profile  my-profile 


