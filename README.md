Create a CloudFormation template to automate full CI/CD process to deploy on ECS

Resources Needed: 
    ➢ AWS CodePipeline 
    ➢ AWS ECR 
    ➢ AWS VPC with 2 Subnets 
    ➢ Application Load Balancer 
    ➢ Internet Gateway 
    ➢ Fargate ECS Cluster

Objective: Deploy the CI/CD Pipeline using a Cloudformation template and once it succeeds on creating the Docker image, deploy the next Cloudformation template containing the Fargate ECS Cluster infrastructure using this pipeline itself.

AWS CodePipeline: Used to build and deploy the application along with the AWS Infrastructure needed.

Stages: 
➢ Source: Stage where the code exists. We are using GitHub here. 
➢ Build: Stage where the Source code is compiled and any packages are installed. Here, we are using to build the docker image and push it to ECR. It outputs the ECR URL saved in a S3 bucket so that deploy stage can use it. 
➢ Deploy: Stage where the deployment will be done. Here, we are using CloudFormation as deployment provider which can be used to create the ECS Fargate infrastructure to deploy the application.

Main Steps of Deployment process:

➢ Deploy the CloudFormation template to create CodePipeline Infrastructure.
➢ Once the CloudFormation Stack is deployed, CodePipeline pulls the code from the GitHub in the Source Stage.
➢ CodePipeline builds the docker image and pushes to ECR in the build stage using the AWS CodeBuild Service.
➢ CodePipeline starts the deployment of the CloudFormation template to deploy the ECS Infrastructure.
Template1 (CodePipeline.yaml): Createa the following resources to get the CI/CD Infrastructure. ➢ ECR Repository ➢ S3 Bucket ➢ IAM Role for CodePipeline Execution ➢ IAM Role for CodeBuild Execution (Build Stage) ➢ IAM Role for CloudFormation Execution (Deploy Stage) ➢ AWS BuildProject ➢ AWS CodePipeline