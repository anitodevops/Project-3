# Dockerization

Containerize the application and verify that it runs on port 3000.

### Create Dockerfile 

[Dockerfile](https://github.com/anitodevops/Project-3/blob/main/Dockerfile)

*By default nginx listen to port 80 , to modify that create the default.conf file and push it to **/etc/nginx/conf.d/***

### Config File

[default.conf](https://github.com/anitodevops/Project-3/blob/main/default.conf)

### Build docker image

`docker build -t mindtrack-image:latest . `

### View docker images

`docker images`

### Run docker container using docker image.

`docker run -d --name app-cont -p 3000:3000 mindtrack-image:latest`

### View running docker containers 

` docker ps `

![dockerimg](https://github.com/anitodevops/Project-3/blob/main/Images/Docker%20Build%20%26%20Run.png)

Browser verification : http://15.206.211.212:3000

![dockeroutput](https://github.com/anitodevops/Project-3/blob/main/Images/App%20run%20on%20Docker%20cont%20public%20IP.png)
