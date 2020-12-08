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
