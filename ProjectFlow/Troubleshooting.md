# Troubleshooting

**To view specific pipeline execution :**

aws codepipeline get-pipeline-execution  --pipeline-name mindtrack-pipeline  --pipeline-execution-id 0f907e6e-34b8-4ce5-9186-81db05f6d443  --region ap-south-1

**To view execution failures:**

aws codepipeline list-action-executions  --pipeline-name mindtrack-pipeline  --region ap-south-1

**To check execution logs :**

aws logs get-log-events \

--log-group-name "/aws/codepipeline/mindtrack-pipeline" \

--log-stream-name "execution-id" \

--region ap-south-1

**To check iam role policices attached**

aws iam list-attached-role-policies --role-name AWSCodePipelineServiceRole-ap-south-1-mindtrack-pipe

**To check for application logs:**

kubctl logs <podname>

