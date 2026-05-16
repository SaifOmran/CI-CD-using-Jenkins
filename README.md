# 🚀 Jenkins Shared Library CI/CD Project

## 📌 Overview

This project demonstrates a complete CI/CD workflow using �entity["software","Jenkins","CI/CD automation server"] Shared Libraries for multiple Spring Boot applications.

The main goal of this project is to avoid duplicating Jenkins pipeline code across applications by creating a reusable shared pipeline.

The same shared library is used to build, package, dockerize, push, and deploy **3 different Spring Boot applications**.

---

# 🏗️ Architecture

```text
                    +--------------------------+
                    |  Jenkins Shared Library  |
                    |     buildApp.groovy      |
                    +------------+-------------+
                                 |
        ---------------------------------------------------
        |                        |                        |
        v                        v                        v

   Spring App 1            Spring App 2            Spring App 3
    Jenkinsfile             Jenkinsfile             Jenkinsfile
```

Each application contains only a lightweight `Jenkinsfile` that calls the shared library.

---

# ⚙️ Technologies Used

* Java 17
* Spring Boot
* Maven
* Docker
* Jenkins Shared Library
* Docker Hub
* AWS EC2
* Terraform

---

# 📂 Shared Library Structure

```text
shared-lib/
│
├── vars/
│   └── buildApp.groovy
│
└── README.md
```

---

# 🔥 Shared Pipeline Responsibilities

The shared library handles:

✅ Cloning source code

✅ Building Maven projects

✅ Creating Docker images

✅ Tagging Docker images

✅ Pushing images to Docker Hub

✅ Deploying containers automatically

---

# 🧠 Shared Library Example

```groovy
buildApp(

    PORT: '8071',

    REPO_URL: 'https://github.com/example/app',

    IMAGE_NAME: 'app',

    IMAGE_TAG: 'v1',

    REPO_NAME: 'saif/api',

    CONTAINER_NAME: 'petclinic-container'
)
```

---

# 📄 Example Jenkinsfile

Each application uses a minimal Jenkinsfile:

```groovy
@Library('shared-lib@main') _

buildApp(

    PORT: '8071',

    REPO_URL: 'https://github.com/example/app',

    IMAGE_NAME: 'app',

    IMAGE_TAG: 'v1',

    REPO_NAME: 'saif/api',

    CONTAINER_NAME: 'petclinic-container'
)
```

---

# 🐳 Dockerfile Example

```dockerfile
FROM eclipse-temurin:17-jre

WORKDIR /app

COPY target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

# 🐳 Docker Workflow

```text
docker build
docker tag
docker push
docker run
```

Example image:

```text
saif/api:v1
```

---

# ☁️ Infrastructure Provisioning

Terraform provisions:

* Jenkins Master EC2
* Jenkins Agent EC2
* Security Groups
* Elastic IPs
* 100GB EBS Volumes

---

# 🔐 Jenkins Configuration

## Required Tools

### Maven

```text
Manage Jenkins → Tools → Maven Installations
```

### JDK

```text
Manage Jenkins → Tools → JDK Installations
```

---

# 🔑 Required Credentials

## Docker Hub Credentials

Add Docker Hub credentials:

```text
Manage Jenkins → Credentials
```

Type:

```text
Username with password
```

Credentials ID:

```text
docker-cred
```

---

# 🖥️ Jenkins Agent Configuration

The Jenkins agent connects using SSH.

Example remote root directory:

```text
/home/ec2-user/jenkins
```

---

# 📋 Pipeline Stages

```text
Clone
Build
Build Image
Push Image
Deploy
```

---

# 🚀 Future Improvements

* Kubernetes deployment
* Helm charts
* SonarQube integration
* Multi-environment deployment
* Automated rollback
* Slack notifications

---

# 👨‍💻 Author

Developed by �entity["people","سيف عمران","Saif Omran"]
