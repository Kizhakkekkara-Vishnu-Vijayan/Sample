# Backend configuration (RABBITMQ, TOMCAT) 
## 1. RABBITMQ Configuration
### Login to the RABBITMQ vm
>  **$ vagrant ssh rmq01**
### Verify Hosts entry, if entries missing update it with IP and hostnames
>  **# cat /etc/hosts**
### Update OS with latest patches
>  **# yum update -y
### Set EPEL Repository
>  **# yum install epel-release -y
### Install Dependencies
```
# sudo yum install wget -y
# cd /tmp/
# dnf -y install centos-release-rabbitmq-38
# dnf --enablerepo=centos-rabbitmq-38 -y install rabbitmq-server
# systemctl enable --now rabbitmq-server
```
### Setup access to user test and make it admin
```
# sudo sh -c 'echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config'
# sudo rabbitmqctl add_user test test
# sudo rabbitmqctl set_user_tags test administrator
# sudo systemctl restart rabbitmq-server
```
## 2. TOMCAT Configuration
### Login to the tomcat vm
>  **$ vagrant ssh app01**
### Verify Hosts entry, if entries missing update the it with IP and hostnames
>  **# cat /etc/hosts**
### Update OS with latest patches
>  **# yum update -y**
### Set Repository
>  **# yum install epel-release -y**
### Install Dependencies
>  **# dnf -y install java-11-openjdk java-11-openjdk-devel**

>  **# dnf install git maven wget -y**

### Change dir to /tmp
>  **# cd /tmp/**
### Download & Tomcat Package
>  **# wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.75/bin/apache-tomcat-9.0.75.tar.gz**

> **# tar xzvf apache-tomcat-9.0.75.tar.gz**

### Add tomcat user
> **# useradd --home-dir /usr/local/tomcat --shell /sbin/nologin tomcat**

### Copy data to tomcat home dir
> #### # cp -r /tmp/apache-tomcat-9.0.75/* /usr/local/tomcat
### Make tomcat user owner of tomcat home dir
> **# chown -R tomcat.tomcat /usr/local/tomcat**
## _Setup systemctl command for tomcat_
### Create tomcat service file
> **# vi /etc/systemd/system/tomcat.service**
## Update the file with below content
```
[Unit]
Description=Tomcat
After=network.target
[Service]
User=tomcat
WorkingDirectory=/usr/local/tomcat
Environment=JRE_HOME=/usr/lib/jvm/jre
Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_HOME=/usr/local/tomcat
Environment=CATALINE_BASE=/usr/local/tomcat
ExecStart=/usr/local/tomcat/bin/catalina.sh run
ExecStop=/usr/local/tomcat/bin/shutdown.sh
SyslogIdentifier=tomcat-%i
[Install]
WantedBy=multi-user.target
```
### Reload systemd files
> **# systemctl daemon-reload**
### Start & Enable service
> **# systemctl start tomcat**

> **# systemctl enable tomcat**
## CODE BUILD & DEPLOY (app01)
### Download Source code
> **# git clone https://github.com/Kizhakkekkara-Vishnu-Vijayan/Clone-directory.git**
### Update configuration
```
# cd Clone-directory
# vim src/main/resources/application.properties
# Update file with backend server details
```
## Build code
### Run below command inside the repository (Clone-directory)
> **# mvn install**
## Deploy artifact
```
systemctl stop tomcat**
# rm -rf /usr/local/tomcat/webapps/ROOT*
# cp target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
# systemctl start tomcat
# chown tomcat.tomcat /usr/local/tomcat/webapps -R
# systemctl restart tomcat
```

