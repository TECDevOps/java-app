## Java Login App ##
Testing 

## Sample Java Login application uses "UserDB" database and Table schema to store the Employee Login details. ##

## How to see list of Databases ##
SHOW DATABASES;

## How to create Database ##

CREATE DATABASE UserDB;

## How to list Tables ##

USE UserDB;

SHOW TABLES;

## How to create Table ##
## Below Query to create require TABLE schema to store Employee records ##

CREATE TABLE Employee (
  id int unsigned auto_increment not null,
  first_name varchar(250),
  last_name varchar(250),
  email varchar(250),
  username varchar(250),
  password varchar(250),
  regdate timestamp,
  primary key (id)
);

## List Table data ##
SELECT * FROM Employee;

## Describe Table schema ##
DESCRIBE Employee;
# java-app
# java-app
# java-app
==========================================================================================
Welcome back, Reader.  This article explains how to Build and Run Java Web Application into Tomcat Runtime environment.

TABLE OF CONTENTS
Infrastructure Setup
Build
Deployment
Validation
Infrastructure Setup
1. Create two EC2 instances on AWS cloud to Build the source and then Run the application.

1. JDK 1.8 or above must be installed and configured to Build and Deploy Java applications. Hence, Run below commands to setup JDK [Java Development Kit] on both Build and Deploy servers.

Download JDK Binary

cd /opt
wget https://download.java.net/openjdk/jdk11/ri/openjdk-11+28_linux-x64_bin.tar.gz
tar -zxvf openjdk-11+28_linux-x64_bin.tar.gz
Define PATH variable in /etc/profile as below

export JAVA_HOME=/opt/jdk-11
export PATH=$PATH:/opt/jdk-11/bin
Verify JAVA version

java –version
2. Download and Install Apache Maven on Build Server

Download Maven Binary

cd /opt
wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.zip
unzip apache-maven-3.8.6-bin.zip
Define PATH variable in /etc/profile as below

export M2_HOME=/opt/apache-maven-3.8.6
export PATH=$PATH:/opt/apache-maven-3.8.6/bin
Verify JAVA version

mvn –version
3. Download and Install Apache Tomcat on App server

Download Tomcat Binary

cd /opt
wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.83/bin/apache-tomcat-8.5.83.zip
unzip apache-tomcat-8.5.83.zip
cd /opt/apache-tomcat-8.5.83/bin/
chmod +x ./*
Build
Login to Build Server and clone the Bitbucket source code repository
cd /opt
git clone https://dptrealtime@bitbucket.org/dptrealtime/java-login-app.git
Build the Java Source
cd /opt/java-login-app
mvn package
Verify that artifacts .war are created in ‘target’ folder
ls -l target
Deployment
During the Build step artifacts were created in Build Server target directory. Need to copy the Maven Artifact .war to Tomcat  webapps directory
Login to Build server copy the .war to app server [Example command as below]
scp dptweb-1.0.war ec2-user@54.242.160.214:/opt/apache-tomcat-8.5.83/webapps
Start Tomcat Services
/opt/apache-tomcat-8.5.83/bin
 ./catalina.sh start
Verify that port 8080 is in LISTEN state
netstat -tupln | grep -i 8080
Validation
Browse the application from internet browser by sending the http request to Port 8080 as below. Here “dptweb-1.0” is the application name deployed into Tomcat webapps.

http://54.242.160.214:8080/dptweb-1.0/

If the Server IP is already configured as A record in the DNS then, You should be now able to access the web application using the domain like below.

http://www.edshopper.com:8080/dptweb-1.0/

Goal of this article to understand the simple Java Web application Build and Deployment process to Run the application in Tomcat runtime environment.  Hope this article helps!
