# Monitor & Log with AWS CloudWatch

Monitoring the application and pipeline execution using CloudWatch Log groups .

Since we have addd the CloudWatchFullAccess policy to Code build , Pipeline & added admin policy EKS cluster logs are updated in respective log groups.

Cloud Watch Log groups

![loggroups](https://github.com/anitodevops/Project-3/blob/main/Images/CloudWatch%20Log%20Groups.png)

LoadBalancer - Node Health Check 

![LB](https://github.com/anitodevops/Project-3/blob/main/Images/LB%20DNS%20Node%20Health%20check.png)

CodeBuild Logs for MindTrack-build

![buildlogs](https://github.com/anitodevops/Project-3/blob/main/Images/Mindtrack-build%20CloudWatch%20Logs.png)

CodeBuild Logs for MindTrackbuild-deploy

![deploylogs](https://github.com/anitodevops/Project-3/blob/main/Images/mindtrackbuild-deploy%20Cloudwatch%20Logs%20.png)

Codepipeline Logs for MindTrack-pipeline

![pipelinelogs](https://github.com/anitodevops/Project-3/blob/main/Images/mindtrack-pipeline%20CloudWatch%20Logs.png)

