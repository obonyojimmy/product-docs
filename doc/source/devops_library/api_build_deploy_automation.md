### Introduction 

#### 1)Standard project(mule version 3.8.1 CE) structure for API:
~~~
https://gitlab.com/omicmd/galaxy-api.git 
galaxy-api
 	src/main
 	....
 	..
 	pom.xml
 
~~~


#### 2)pom.xml should contain groupId , artifactId and version consistant as following for galaxy corresponding to api project   
~~~ 
    <groupId>com.omicmd.galaxy</groupId>
	<artifactId>system-api-galaxy</artifactId>
    <version>1.0.0-SNAPSHOT</version>                   
~~~


#### 3)Jenkins: for each api we can one folder in Jenkins 

##### Containing jobs:
~~~
Builder Job : http://ec2-52-88-165-178.us-west-2.compute.amazonaws.com/job/galaxy-api/job/galaxy_snapshot_builder/  
Deploy Job :http://ec2-52-88-165-178.us-west-2.compute.amazonaws.com/job/galaxy-api/job/galaxy-api-deploy/
API health check Job :http://ec2-52-88-165-178.us-west-2.compute.amazonaws.com/job/galaxy-api/job/galaxy_api_healthcheck/ 
~~~ 
 
Jenkins test User:

~~~
User: testuser  
Password: testuser123
~~~ 
 

### Mule in Docker

#### Docker Briefly

In short, Docker allows for creating of images that serve as blueprints for containers. A Docker container is an instance of a Docker image in the same way a Java object is an instance of a Java class.
~~~
FROM williamyeh/java8

MAINTAINER dksingh3117@gmail.com


RUN cd /opt && wget https://repository.mulesoft.org/nexus/content/repositories/releases/org/mule/distributions/mule-standalone/3.8.1/mule-standalone-3.8.1.tar.gz
RUN cd /opt && tar xvzf mule-standalone-3.8.1.tar.gz
#RUN echo "081530788032f2af7fe1593bd6030f25 /opt/mule-standalone-3.8.1.tar.gz" | md5sum -c
#RUN rm ~/mule-standalone-3.8.1.tar.gz
RUN ln -s /opt/mule-standalone-3.8.1 /opt/mule

CMD [ "/opt/mule/bin/mule" ]
~~~

The resource isolation features of Linux are used to create Docker containers, which are more lightweight than virtual machines and are separated from the environment in which Docker runs, the host.

#### Prerequisites
Ubuntu:
14.04 (64-bit)

#### Installing Docker
The simplest way to install Docker is to use an installation script made available at the Docker website:
~~~


curl -sSL https://get.docker.com/ubuntu/ | sudo sh
~~~
If you are not running Ubuntu or if you do not want to use the above way of installing Docker, please refer to this page containing instructions on how to install Docker on various platforms.
To verify the Docker installation, open a terminal window and enter:

~~~
sudo docker version
~~~

#### Files and Docker Containers

As part of this exercise we also set up the directories in the host operating system that are going to be shared with the Docker container.

- In your home directory, create a directory named “mule-root”.
- In the “mule-root” directory, create three directories named “apps”, “conf” and “logs”.
- Download the Mule CE 3.8.1 standalone distribution.
- From the Mule CE 3.8.1 distribution, copy the files in the “apps” directory to the “mule-root/apps” directory you just created.
- From the Mule CE 3.8.1 distribution, copy the files in the “conf” directory to the “mule-root/conf” directory you created.

The resulting file- and directory-structure should look like this (shown using the tree command):
~~~
~/mule-root/
├── apps
│   └── default
│       └── mule-config.xml
├── conf
│   ├── log4j.properties
│   ├── tls-default.conf
│   ├── tls-fips140-2.conf
│   ├── wrapper-additional.conf
│   └── wrapper.conf
└── logs
~~~

#### Deploy the Mule Application

[API_NAME]_snapshot_builder jenkins job  will build api project and achived into [API_NAME].[SEMVER].[BUILD_NUMBER].zip 

[API_NAME]_api_deploy jenkins job will do SCP and create dockerized mule container with corresponding 
 API

docker container will look like following 

~~~
CONTAINER ID        IMAGE                             COMMAND                CREATED             STATUS              PORTS                    NAMES
c85558a7132e        mule:system-api-ehrfhir-1.3.2.1   "/opt/mule/bin/mule"   About an hour ago   Up About an hour    0.0.0.0:8081->8081/tcp   blissful_lewin
u
~~~

#### Slack notification 

Both Builder and deployer Job will send notification (sucess, fail and unstable)

Message will look like following 
~~~
fhir_api » galaxy_snapshot_builder - #1 Success after 1 min 5 sec (Open)
Build #1 from branch origin/master.


fhir_api » fhir-api-deploy - #38 Unstable after 2 min 6 sec (Open)
Deployment to mule Container is unstable or failing, please find find the log below. 
ERROR LOG LINK:https://s3-us-west-2.amazonaws.com/system-api-ehrfhir/api_error.log
Mule Log : https://s3-us-west-2.amazonaws.com/system-api-ehrfhir/mule.log
API Link:http://ec2-52-77-217-204.ap-southeast-1.compute.amazonaws.com:8081/api/Patient/Patient-1125
~~~




