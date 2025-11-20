#  AWS CodeBuild

## Build using CodeBuild 

### Create S3 Bucket to Build Artifacts
AWS S3 -> Click create Bucket -> Create an S3 bucket -> choose general purpose ;  enter name - mindtrack-artifacts ; enable block public access , choose SSM-KMS encryption , disable versioning -> click create 

![S3](https://github.com/anitodevops/Project-3/blob/main/Images/S3%20bucket-%20Codebuild%20artifacts.png)

### Create IAM Role & Attach Policies 

**IAM role & Policies:**
**Role :** CodebuildforMindtrackbuild
**Policies:**
 - AmazonEC2ContainerRegistryFullAccess 
 -  AmazonS3FullAccess
 - AWSCodeBuildAdminAccess
 - CloudWatchFullAccess
 
![codebuild](https://github.com/anitodevops/Project-3/blob/main/Images/IAM%20Role%20-%20Codebuild.png)

## CodeBuild Setup 

![step1](https://github.com/anitodevops/Project-3/blob/main/Images/CodeBuild%20Setup%20-%201.png)

![step2](https://github.com/anitodevops/Project-3/blob/main/Images/CodeBuild%20Setup%20-%202.png)

![step3](https://github.com/anitodevops/Project-3/blob/main/Images/CodeBuild%20Setup%20-%203.png)

![step4](https://github.com/anitodevops/Project-3/blob/main/Images/CodeBuild%20Setup%20-%204.png)

![mindtrackbuild](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrack-build.png)

Automating Image build and Push to EKS Cluster using CodeBuild **[buildspec.yml](https://github.com/anitodevops/Project-3/blob/main/buildspec.yml)**

Push yaml file  to Git Repo to trigger build.

![build-1](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrack-build%20Build-1%20Phase%20details.png)

![imagepush](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrack-build-image%20push%20to%20ECR.png)

![artifacts](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrack-build-BuildArtifacts.png)

