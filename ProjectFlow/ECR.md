# Image Push to Amazon ECR

Tag & Push the docker image to Elastic Container Registry.

## Create ECR Repo 

- Name : *project3/mindtrack-app*
- Repo URI: *224679997553.dkr.ecr.ap-south-1.amazonaws.com/project3/mindtrack-prod*

![ECRrepo](https://github.com/anitodevops/Project-3/blob/main/Images/ECR%20Repo%20Creation.png)

## Connect to AWS account.
```
aws configure

AWS Access Key ID [None]:  AKI***********52
AWS Secret Access Key [None ]: j5Hfu*************************Lpq
Default region name [ap-south-1]: ap-south-1
Default output format [json]: json
```
## Login to AWS ECR

 Use  Push Commands shown in ECR repository to connect build , tag  & push image to the repository.
 ![Cmds](https://github.com/anitodevops/Project-3/blob/main/Images/ECR%20Repo%20Push%20Commands%20.png)
 
```
Connect to ECR:
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 224679997553.dkr.ecr.ap-south-1.amazonaws.com

Tag the image as per ECR repo uri:
docker tag mindtrack-image:latest 224679997553.dkr.ecr.ap-south-1.amazonaws.com/project3/mindtrack-prod:latest

Push image to ECR:
docker push 224679997553.dkr.ecr.ap-south-1.amazonaws.com/project3/mindtrack-prod:latest
```
![imgpush](https://github.com/anitodevops/Project-3/blob/main/Images/image%20push%20to%20ECR%20Repo.png)

![ECR](https://github.com/anitodevops/Project-3/blob/main/Images/Image%20in%20EC%20Repo.png)

