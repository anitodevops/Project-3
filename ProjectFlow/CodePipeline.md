# CI/CD with CodePipeline 

Automating complete CI/CD using AWS CodePipeline , deploy using AWS EKS Provider using kubectl.

**Overall Flow :**
 1. CodePipeline to deploys code maintained in a  **Github repository** to the  **EKS cluster**. 
 2.  This  pipeline is  **triggered**  when a code push is made to the  **Github repository**.  
 3. The pipeline deploys your changes to an Amazon EKS instance using Pipelines - Deploy stage  using the K8s' Objects.

### Create IAM Role & Attach Policies 

**IAM role & Policies:**
**Role :** AWSCodepipelineServiceRole-p-south-1-mindtrack-pipe
**Policies:**

![iampipeline](https://github.com/anitodevops/Project-3/blob/main/Images/IAM%20Role%20-%20Mindtrack%20Pipeline%20.png)

### Setup EKS Admin Policy

Go to EKS cluster dashboard ->click Access tab -> create -> 

**Configure IAM access entry:**
choose IAM principal ARN -> select the codepipeline-mindtrack-pipe role , type-standard->next

![step-1](https://github.com/anitodevops/Project-3/blob/main/Images/EKS%20Admin%20Policy%20Setup%20-1.png)

**Add Access Policy :**
 choose ->EKSadminploicy -> choose Kubernetes namesspace ->click add a namespace ->default-> click create.  
 
![step-2](https://github.com/anitodevops/Project-3/blob/main/Images/EKS%20Admin%20Policy%20Setup%20-2.png)

**Updated Cluster Policy  :**

![step-3](https://github.com/anitodevops/Project-3/blob/main/Images/EKS%20Cluster%20-%20add%20EKSAdminPolicy.png)

### Setup CodePipeline
#### creation option
- Create pipeline -> build custom pipeline -> OK

![step-1](https://github.com/anitodevops/Project-3/blob/main/Images/codepipeline%20Setup-1.png)

#### pipeline settings
- Enter pipeline name - Mindtrack-pipeline 
- Choose new service role -> auto creates the role& policy

![step-2](https://github.com/anitodevops/Project-3/blob/main/Images/codepipeline%20Setup-2.png)

####  Source Stage
- Choose Source -> Github App 
-  Repository name & branch 
-  Enable webhooks (by default)

![step-3](https://github.com/anitodevops/Project-3/blob/main/Images/codepipeline%20Setup-3.png)

CodePipeline is connected to your GitHub repository.
Any push made to the main branch triggers the pipeline automatically.
Source artifact (ZIP) is passed to the Build stage.

#### build stage
- Choose buildstage -> AWS codebuild 
- project name - mindtrack-build 
- Input artifacts - source artifacts  

![step-4](https://github.com/anitodevops/Project-3/blob/main/Images/codepipeline%20Setup-4.png)

CodeBuild reads the buildspec.yml file.
Authenticate to Amazon Elastic Container Registry.
Builds the Docker image using Dockerfile.
Tags the image to the ECR RepoURI - mindtrack-prod
Pushes the image to ECR repository.
Updates the  deployment.yaml by fetching the new ECR image URI.
Stores updated Kubernetes manifests as the Build Artifact for Deploy stage.

#### test stage
- Skip test stage

#### deploy stage
- Deploy stage -> Amazon EKS -> input artifacts (build artifact)
- Choose cluster -> mindtrack
- Deploy config type -> kubectl 
- Manifest file paths -> deployment.yaml,service.yaml ( give commas after each file)

![step-5](https://github.com/anitodevops/Project-3/blob/main/Images/codepipeline%20Setup-5.png)

Pipeline uses a custom deploy EKS provider to deploy using kubectl by Connecting to the EKS cluster.
Fetches the manifest files deployment.yaml and service.yaml from the Build Stage Artifact.
Checks if the deployment is available 
if deployment exists Updates image inside deployment manifest & rollouts the chnages.
if not available runs & creates the deployments & service.
Loadbalancer gets created/Updated automatically,
Application becomes available publicly through the LoadBalancer URL.

#### Review & create Pipeline 

![pipeline](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrack-pipeline.png)

**Three Pipeline Stages:**

-   A source stage  **(Source)**  for your Github source action.
- A  build stage **(Build)** for Codebuild to build & pushing docker image to ECR.
-   A deploy stage  **(Deploy)**  for your CodeDeploy via AWS EKS provider.

### Test run the pipeline & push a readme file to Git to trigger pipeline 

Git push -> trigger pipeline -> codebuild-> code deploy to EKS.

![testpipe](https://github.com/anitodevops/Project-3/blob/main/Images/mindtrack-pipeline%20Trigger%20via%20Git%20Push%20.png)

#### check service  `Kubectl get svc`
 
#### check pod logs `kubectl logs <pod-name>`
 
![pod logs](https://github.com/anitodevops/Project-3/blob/main/Images/Application%20Logs%20-%20Pod%20.png)

Use LoadBalancer URL to verify App Running on port :3000

![Deployment](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrack-pipeline%20-%20Applicaation%20Deployment.png)

