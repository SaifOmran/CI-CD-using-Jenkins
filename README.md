Spring Boot Shared Library CI/CD
Overview

This project demonstrates a complete CI/CD workflow using Jenkins Shared Libraries for multiple Spring Boot applications.

The goal is to avoid duplicating pipeline logic across projects by creating a reusable Jenkins Shared Library that handles:

Cloning source code
Building Maven projects
Creating Docker images
Pushing images to Docker Hub
Deploying containers automatically

The same shared pipeline is used by 3 different applications.

Architecture
                    +----------------------+
                    | Jenkins Shared Lib   |
                    |  buildApp.groovy     |
                    +----------+-----------+
                               |
         -------------------------------------------------
         |                    |                         |
         v                    v                         v

   Spring App 1         Spring App 2             Spring App 3
   Jenkinsfile          Jenkinsfile              Jenkinsfile

Each application contains only a lightweight Jenkinsfile that calls the shared library.

Technologies Used
Java 17
Spring Boot
Maven
Docker
Jenkins Shared Library
Docker Hub
AWS EC2
Terraform
Shared Library Structure
shared-lib/
│
├── vars/
│   └── buildApp.groovy
│
└── README.md
Shared Pipeline Responsibilities

The shared library pipeline performs:

Clone application repository
Build application using Maven
Build Docker image
Tag Docker image
Push image to Docker Hub
Deploy container

Jenkins Configuration
Required Tools

Configure the following tools in Jenkins:

Maven
Manage Jenkins → Tools → Maven Installations
JDK
Manage Jenkins → Tools → JDK Installations
Required Credentials
Docker Hub Credentials

Add Docker Hub credentials:

Manage Jenkins → Credentials

Type:
Username with password
Credentials ID:
docker-cred

Terraform Infrastructure
Terraform provisions:
Jenkins Master EC2
Jenkins Agent EC2
Security Groups
Elastic IPs
100GB storage volumes
Jenkins Agent
