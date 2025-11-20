# AWS CodeDeploy 

## Deploy using CodeBuild with deployspec.yml

### Create IAM Role & Attach Policies 

**IAM role & Policies:**
**Role :** CodebuildforMindtrackbuild-deploy
**Policies:**
- AmazonEKSClusterPolicy
- AmazonEKSWorkerNodePolicy
- AmazonEC2ContainerRegistryReadOnly
- AWSCodeBuildDeveloperAccess
- AmazonS3ReadOnlyAccess
- CloudWatchFullAccess
- Custom create policy **AWSEKSDeployAccessforCodebuild-deploy**  as inline policy to connect or authenticate with the cluster.
	- Eks:describecluster         -> To fetch cluster name, endpoint
	- Sts:getcallidentity	   ->  for aws CLI(kubeconfig) to verify IAM role that codebuild calls & generate EKS Auth Token

```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Allow",
			"Action": [
				"eks:DescribeCluster",
				 "sts:GetCallerIdentity"
			],
			"Resource": [
				"*"
			]
		}
	]
}
```
![build-deploy](https://github.com/anitodevops/Project-3/blob/main/Images/IAM%20Role%20-%20Codebuild-deploy.png)

## Codebuild-deploy setup 

![step1](https://github.com/anitodevops/Project-3/blob/main/Images/Codebuild-deploy%20Setup%20-1.png)

![step2](https://github.com/anitodevops/Project-3/blob/main/Images/Codebuild-deploy%20Setup%20-2.png)

![step3](https://github.com/anitodevops/Project-3/blob/main/Images/Codebuild-deploy%20Setup%20-3.png)

Automating Image Pull & deploying to EKS cluster using Codebuild **[deployspec.yaml](https://github.com/anitodevops/Project-3/blob/main/deployspec.yml)**

Code passes all three scenarios:
 - when no deployment is available - creates deployment 
 - when the image tag is diff - updates image tag & redeploys
 - when image tag is same as the previous - still restarts deployment.

Update configmap file to maprole of codebuild-deploy

`kubectl edit configmap aws-auth -n kube-system`

![configmap](https://github.com/anitodevops/Project-3/blob/main/Images/Configmap%20update%20fo%20Mindtrackbuild-deploy.png)

Verify roles:

`kubectl describe configmap aws-auth -n kube-system `

![deploy-1](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrackbuild-deploy-build-1.png)

![details-1](https://github.com/anitodevops/Project-3/blob/main/Images/mindtrackbuild-deploy%20Build-1%20phase%20details.png)

To restart the deployment added rollout restart.

`kubectl rollout restart deployment/mindtrack-deploy`

Push deployspec.yml to git to trigger build.
Check Service LB url is updated ensures that new deployment has been created.

![svccheck](https://github.com/anitodevops/Project-3/blob/main/Images/mindtrackbuild-deploy%20Svc%20check%20.png)

Application LB check :

![LB-URL](https://github.com/anitodevops/Project-3/blob/main/Images/App%20LB%20Url%20Verification.png)

