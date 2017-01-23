# Docker Compose file to create containers for Jenkins, SonarQube and Nexus

##Setup an AWS EC2 instance.

```
sudo yum update -y
sudo yum install -y docker
sudo yum install -y git
sudo service docker start
sudo usermod -a -G docker ec2-user
sudo curl -L "https://github.com/docker/compose/releases/download/1.9.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

```

###Log out and log back in again to pick up the new docker group permissions.

```
docker info
git clone https://github.com/muralibala/docker-compose-jenkins-nexus-sonar.git
cd docker-compose-jenkins-nexus-sonar/
docker-compose up
curl http://localhost:8080

```

###In case of failure, run a test each image individually.
##Make sure to give jenkins user privileges to jenkins directory
```
sudo chown 1000 jenkins
docker run -d -p 8080:8080 --name=jenkins-master jenkins -v $(pwd)/jenkins:/var/jenkins_home
docker run -d -p 8081:8081 --name=nexus sonatype/nexus:oss
```
