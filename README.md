In this project we will deploy a 3-tier application to an EC2 server using a CI/CD pipeline set up on Jenkins. On the EC2 instance we will have the following installed

- Jenkins
- Docker
- Build tools (npm,nodejs)
- Git

# Configure application code
* Clone the code needed for CICD
* Create branches for demo
* Create Dockerfile to build docker image and push to private repo 


# Configure AWS

## Create Admin user
Give programmatic & Console access

Add user to group

Admin-Administrator policy

Save info and keys securely

## Provision EC2 instance (Deploy  web app on EC2)
**Launch instance** 

* Choose base image

* Choose instance type - t2 micro

* Configure network (leave defaults)

* Add storage (leave defaults)

* Add Tags(web server with Docker/leave defaults)

* Configure security group - create new

* Name: Security-group-docker-server
            
            
## Connect to EC2 instance with SSH
Select an existing key pair or create new one. Save the private key pair file to .ssh folder

`my downloads/docker-server.pem ~/.ssh/`

Change permission to read only 

```
ls -l  
chmod 400 .ssh/devops-server.pem
```

SSH into the server with the saved key as the ec2-user created.


## Install Docker on EC2 instance

Update the package manager tool for up to date repositories and install docker.
```
sudo yum update
sudo yum install docker
docker --version
```

start docker daemon
```
sudo service docker start
```

Check if docker is running
```
ps aux | grep docker
```

Add ec2-user to docker group (to execute docker cmds)    

```
sudo usermod -aG docker ec2-user
```

Confirm group has been created and check containers (exit first then ssh again)
```
groups
docker ps
```      
    
## Install Jenkins on EC2 server
## Install git on the running server   

# Configure Jenkins
**Install build tools (npm,nodejs)**

Install node and npm on the server. Confirm the distribution of the linux server so as to download the correct binaries 

    --cat /etc/issue

Follow documentation to install node binaries on the specific OS the server is running.

**Connect to github**

Configure credentials for SCM with Jenkins credentials provider to authenticate to github.

Create webhook for build triggers

**Create Jenkinsfile to build pipeline**

Create multi-branch pipeline

Configure Jenkinsfile to build and deploy to server

* Test

* Build

* Push artifact to docker hub 

* Deploy application on a development server

**Deploying application on the server**

On server, configure firewall rule to allow Jenkins server IP as a source for SSH. Allow access from Jenkins IP address. 
Give Jenkins server permission to access EC2 instance (Allow the correct port)

Connect to EC2 server instance from Jenkins server via ssh (ssh agent)

Install **SSH Agent** plugin. Create credentials for EC2. Connect to EC2 instance via multibranch pipeline

Go to credentials and input the details to set up the key. copy pem contents to key and finish. 

These credentials can be used in jenkinsfile to write cmds to execute on EC2 terminal after SSH connection.

Add config in Jenkinsfile (see Jenkinsfile syntax for a plugin) Go to pipeline>pipeline syntax>snippet generator>ssh agent>generate pipeline script>copy syntax

Go to Jenkinsfile and add syntax in deploy stage. Write logic for connecting and executing docker commands. Make sure docker is already logged in and its credentials stored locally in the server.
