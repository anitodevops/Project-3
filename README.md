# PROJECT - 3 MINDTRACK  

## APPLICATION DEPLOYMENT FLOW:


---

## LINKS:
Git Repo Link: https://github.com/anitodevops/Project-3.git
Load Balancer URL:

---

## MINDTRACK-PIPELINE FLOW: (Source → Build → Deploy)

### 1. Source Stage (GitHub → CodePipeline)

CodePipeline is connected to your GitHub repository.
Any push made to the main branch triggers the pipeline automatically.
Source artifact (ZIP) is passed to the Build stage.

### 2. Build Stage (AWS CodeBuild)

CodeBuild reads the buildspec.yml file.
Authenticate to Amazon Elastic Container Registry.
Builds the Docker image using Dockerfile.
Tags the image to the ECR RepoURI - mindtrack-prod
Pushes the image to ECR repository.
Updates the  deployment.yaml by fetching the new ECR image URI.
Stores updated Kubernetes manifests as the Build Artifact for Deploy stage.

### 3. Deploy Stage (AWS EKS Provider using kubectl)

Pipeline uses a custom deploy EKS provider to deploy using kubectl by Connecting to the EKS cluster.
Fetches the manifest files deployment.yaml and service.yaml from the Build Stage Artifact.
Checks if the deployment is available 
if deployment exists Updates image inside deployment manifest & rollouts the chnages.
if not available runs & creates the deployments & service.
Loadbalancer gets created/Updated automatically,
Application becomes available publicly through the LoadBalancer URL.

---

## SETUP INSTRUCTIONS:

### Docker

### ECR

### Kubernetes

### Code build

### Code deploy

### Code pipeline

### Monitoring

