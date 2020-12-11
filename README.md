# DockerCheatSheet

#This CheatSheet is created to practice on CentOS Linux

sudo su - -> Login as Root User 
 
yum update -> Update Centos to latest version

ps -ef | grep docker -- Check if Docker is up and running

sudo yum install -y yum-utils device-mapper-persistent-data lvm2  --> Install Docker Pre-Req

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo --> Add the repository

yum install docker-ce docker-ce-cli containerd.io --> Install Docker


systemctl start docker  -- Command to start docker

systemctl stop docker -- Command to stop docker

systemctl status docker -- Command to check for docker service

wget https://mirrors.estointernet.in/apache/tomcat/tomcat-9/v9.0.40/bin/apache-tomcat-9.0.40.tar.gz


#### List docker images
docker images

#### Docker pull ubuntu image from dockerhub repository
docker pull ubuntu

#### Docker pull centos image from dockerhub repository
docker pull centos

#### Start/Create centos container
docker run -it -d centos

#### Start/Create ubuntu container and give it a name skillrary
docker run -it -d --name skillrary ubuntu

```quote
##### You can execute the command below if you are trying to use systemd commands like systemctl start etc

docker run -it --name c7 --privileged -d c1image /usr/sbin/init 

```
#### Stop Container
docker stop <containerid/name>
docker stop 4b2c5e5a7e26

#### Start Container
docker start <containerid/name>
docker start 4b2c5e5a7e26

#### Remove container
docker rm <containerid/name>
docker rm 4b2c5e5a7e26

#### Remove image
docker rmi <imagename>
docker rmi Ubuntu

#### Save changes to a container as an image
docker commit 7868e9424f42 devops102tomcat

#### Save an image as a compressed file
docker save devops102tomcat > devops102tomcat.rar

#### Load a compressed image file to Docker
docker load --input devops102tomcat.rar

#### Login to docker hub from command prompt
docker login

#### Tag an image to docker hub repository before pushing it to docker hub
docker tag 60c84fa5590a skillrary/devops102

#### Push a local docker image to docker hub
docker push skillrary/devops102

#### Start a container mapping port 9999 with port 8080
docker run -it -p 9999:8080 -d devops102tomcat

#### Build a docker file
docker build -t devopsdockerfile .

#### Get inside docker container
docker exec -it c7 bash

#### Set the limit for each container
docker run -it --cpus=".5" --memory=100m -d centos  --> While starting the conatiner

docker update --cpu-shares 512 -m 300M <containerid/name>  --> After creating the container
[Refer to Complete Reference](https://github.com/skillrary/DockerCompleteReference)




# Kubernetes Installation

## Following instructions from link https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

### 1. mkdir /etc/docker


### 2. Create daemon.json 

cat <<EOF | sudo tee /etc/docker/daemon.json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2",
  "storage-opts": [
    "overlay2.override_kernel_check=true"
  ]
}
EOF

### 3. mkdir -p /etc/systemd/system/docker.service.d

### 4. Execute following command

sudo systemctl daemon-reload
sudo systemctl restart docker

### 5. systemctl enable docker


### 6. Create Kubernetes repo

cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
EOF

### 7. Execute following commands
sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

### 8. Install Kubernetes
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

### 9. Enable kubelet service
systemctl enable --now kubelet

### 10. Check the version after successful installation

kubeadm version
kubectl version
kubelet --version


