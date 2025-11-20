
# Workspace Setup

Configure local workspace , Clone source code from the github repository.

## Create AWS EC2 instance

Choose instance type - t3.medium with 20 GB memory for optimum performance.

![EC2creation](https://github.com/anitodevops/Project-3/blob/main/Images/Worksapce%20EC2%20Creation.png)

### Install Required Packages

 Install docker , awscli, eksctl , kubectl during EC2 creation as a best practice.
 
```
#!/bin/bash

apt-get update

#installing docker
apt-get install -y ca-certificates curl
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
apt-get update
apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose
 
usermod -aG docker ubuntu

systemctl enable docker
systemctl start docker

#installing kubectl
curl -LO https://s3.us-west-2.amazonaws.com/amazon-eks/1.33.0/2025-05-01/bin/linux/amd64/kubectl
chmod +x ./kubectl
mv kubectl /usr/local/bin/	

#installing eksctl
curl -LO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz"
tar -xzf eksct*tar*
mv eksctl /usr/local/bin/
```
Update SG rules Add rules - Custom TCP port 3000 , Source -Anywhere Ipv4 

![EC2info](https://github.com/anitodevops/Project-3/blob/main/Images/Workspace%20info.png)

## Git 
```
git config --global user.name "an******ps"
git config --global user.email an*****ps@gmail.com
git config --list
```
![gitcloneinit](https://github.com/anitodevops/Project-3/blob/main/Images/Git%20clone%20&%20init.png)

