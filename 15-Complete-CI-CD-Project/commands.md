# Commands

This section contains the complete set of commands used to build, test, containerize, and deploy an application through a production-style Jenkins CI/CD pipeline.

---

# Verify Required Tools

Verify Git

```bash
git --version
```

Verify Java

```bash
java --version
```

Verify Maven

```bash
mvn --version
```

Verify Docker

```bash
docker --version
```

Verify Jenkins

```bash
systemctl status jenkins
```

Linux

```bash
sudo systemctl status jenkins
```

---

# Clone Repository

```bash
git clone https://github.com/username/project.git
```

Navigate to the project

```bash
cd project
```

Check repository status

```bash
git status
```

Pull latest changes

```bash
git pull origin main
```

---

# Git Commands

Stage files

```bash
git add .
```

Commit changes

```bash
git commit -m "Update application"
```

Push changes

```bash
git push origin main
```

View commit history

```bash
git log --oneline
```

---

# Maven Commands

Clean project

```bash
mvn clean
```

Compile source code

```bash
mvn compile
```

Run unit tests

```bash
mvn test
```

Package application

```bash
mvn package
```

Install artifact locally

```bash
mvn install
```

Clean and package

```bash
mvn clean package
```

---

# Gradle Commands

Clean project

```bash
gradle clean
```

Build application

```bash
gradle build
```

Run tests

```bash
gradle test
```

Create JAR

```bash
gradle jar
```

---

# Docker Commands

Build image

```bash
docker build -t my-app:v1 .
```

List images

```bash
docker images
```

Run container

```bash
docker run -d --name my-app -p 8080:8080 my-app:v1
```

List running containers

```bash
docker ps
```

Stop container

```bash
docker stop my-app
```

Remove container

```bash
docker rm my-app
```

Remove image

```bash
docker rmi my-app:v1
```

View container logs

```bash
docker logs my-app
```

---

# Docker Hub Commands

Login

```bash
docker login
```

Tag image

```bash
docker tag my-app:v1 username/my-app:v1
```

Push image

```bash
docker push username/my-app:v1
```

Pull image

```bash
docker pull username/my-app:v1
```

---

# SSH Commands

Generate SSH key

```bash
ssh-keygen -t rsa -b 4096
```

Copy public key

```bash
ssh-copy-id user@server-ip
```

Connect to server

```bash
ssh user@server-ip
```

Copy files

```bash
scp target/my-app.jar user@server-ip:/opt/my-app/
```

---

# Docker Deployment

Pull latest image

```bash
docker pull username/my-app:v1
```

Stop existing container

```bash
docker stop my-app
```

Remove existing container

```bash
docker rm my-app
```

Deploy latest image

```bash
docker run -d \
--name my-app \
-p 8080:8080 \
username/my-app:v1
```

---

# Docker Compose

Start services

```bash
docker compose up -d
```

Stop services

```bash
docker compose down
```

Restart services

```bash
docker compose restart
```

View logs

```bash
docker compose logs
```

---

# Jenkins Pipeline Example

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/username/project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t username/my-app:v1 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push username/my-app:v1'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                ssh user@server-ip "
                docker pull username/my-app:v1 &&
                docker stop my-app || true &&
                docker rm my-app || true &&
                docker run -d --name my-app -p 8080:8080 username/my-app:v1
                "
                '''
            }
        }

    }

    post {

        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline failed.'
        }

        always {
            cleanWs()
        }

    }

}
```

---

# Verify Deployment

Check running containers

```bash
docker ps
```

Check application

```bash
curl http://server-ip:8080
```

View logs

```bash
docker logs my-app
```

Check service status

```bash
systemctl status my-app
```

---

# Rollback Commands

Deploy previous image

```bash
docker pull username/my-app:v1
```

Run previous version

```bash
docker run -d \
--name my-app \
-p 8080:8080 \
username/my-app:v1
```

---

# Useful Linux Commands

Current directory

```bash
pwd
```

List files

```bash
ls -la
```

Create directory

```bash
mkdir -p /opt/my-app
```

Disk usage

```bash
df -h
```

Memory usage

```bash
free -h
```

---

# Summary

| Command | Purpose |
|----------|---------|
| `git clone` | Clone repository |
| `git push` | Push source code |
| `mvn clean package` | Build application |
| `mvn test` | Run unit tests |
| `docker build` | Build Docker image |
| `docker push` | Upload image to Docker Hub |
| `ssh` | Connect to deployment server |
| `scp` | Transfer application files |
| `docker run` | Deploy application |
| `docker compose up -d` | Deploy multi-container application |
| `curl` | Verify deployment |
| `cleanWs()` | Clean Jenkins workspace |

---

# Notes

- Verify all required tools before running the pipeline.
- Keep the Jenkinsfile under version control.
- Store secrets using Jenkins Credentials instead of hardcoding them.
- Run automated tests before deployment.
- Tag Docker images with meaningful versions instead of using only `latest`.
- Validate deployments using health checks before marking the pipeline as successful.
- Archive build artifacts and logs for troubleshooting and auditing.
- Use rollback procedures to quickly recover from failed deployments.