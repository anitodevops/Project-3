# PROJECT – 3   Mind Track

![CICD](https://github.com/anitodevops/Project-3/blob/main/Images/cicd.png)

### Table Of Contents 

-	[Goal](https://github.com/anitodevops/Project-3/tree/main#goal)
-	[Pre-Requisites](https://github.com/anitodevops/Project-3/tree/main#pre-requisites)
-	[Application Deployment Architecture](https://github.com/anitodevops/Project-3/tree/main#application-deployment-architecture)
-	[Architecture Overview](https://github.com/anitodevops/Project-3/tree/main#architecture-overview)
-	[Project WorkFlow](https://github.com/anitodevops/Project-3/tree/main#project-workflow)
-	[Links](https://github.com/anitodevops/Project-3/tree/main#links)
-	[Outcome](https://github.com/anitodevops/Project-3/tree/main#project-outcome)
  
## Goal

To deploy the **Mind Track  Application** into a production-ready environment on **port 3000** using AWS ECR,  AWS EKS,  AWS CI/CD   and to seamlessly monitor the Pipeline using AWS CloudWatch logs.

## Pre-Requisites
-	[AWS Account](https://signin.aws.amazon.com/signup?request_type=register)
-	[GitHub Account](https://github.com/)
-	[Source Code](https://github.com/Vennilavan12/Brain-Tasks-App.git)
  
## Application Deployment Architecture 

![Architecture](https://github.com/anitodevops/Project-3/blob/main/Images/Architecture.png)

## Architecture Overview

-	Developer pushes code → GitHub Repository
-	AWS CodePipeline is triggered
-	CodeBuild builds Docker image → pushes to ECR (Elastic Container Registry)
-	CodeDeploy - Instead of deploy service codeBuild deploys the image to EKS Cluster using Kubernetes manifests
	-	Deployment.yaml
	-	Service.yaml
-	CloudWatch Logs monitors the build, deploy, EKS & the application logs
-	The app runs at port 3000 on an EKS LoadBalancer

## Project WorkFlow 

- [Workspace Setup](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/Workspace.md)
  
- [Dockerization](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/Dockerization.md)

- [Image push to Amazon ECR](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/ECR.md)

- [Kubernetes Cluster on Amazon EKS](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/EKS.md) 

- [AWS CodeBuild](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/CodeBuild.md)

- [AWS CodeDeploy](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/CodeDeploy.md)

- [CI/CD with CodePipeline](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/CodePipeline.md)

- [Monitor & Log with AWS CloudWatch](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/CloudWatch.md)
  
- [Troubleshooting](https://github.com/anitodevops/Project-3/blob/main/ProjectFlow/Troubleshooting.md)

## Links

-	Application LoadBalancer URL: http://aob15fc48056e4e409c80c59672d81ab-868196590.ap-south-1.elb.amazonaws.com

## Project Outcome

- Achieved Zero Downtime & deployed the application on Production ready state.
- Fully automated CI/CD pipeline via AWS services (CodePipeline, CodeBuild, ECR, and EKS).
- Enables secure public access via LB and zero-downtime using Kubernetes services 





