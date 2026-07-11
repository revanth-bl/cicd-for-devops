# Commands

This section contains commonly used Docker commands and Jenkins Pipeline snippets for integrating Docker into a CI/CD pipeline.

---

# Verify Docker Installation

```bash
docker --version
```

---

# Verify Docker Compose Installation

```bash
docker compose version
```

Older versions:

```bash
docker-compose --version
```

---

# Verify Docker Service

Linux

```bash
sudo systemctl status docker
```

Windows (PowerShell)

```powershell
Get-Service docker
```

---

# Start Docker Service

Linux

```bash
sudo systemctl start docker
```

---

# Restart Docker Service

Linux

```bash
sudo systemctl restart docker
```

---

# Verify Jenkins User Can Access Docker

Linux

```bash
groups jenkins
```

Add Jenkins to Docker group:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

---

# Verify Docker Information

```bash
docker info
```

---

# Pull Docker Image

```bash
docker pull nginx
```

---

# List Docker Images

```bash
docker images
```

---

# Build Docker Image

```bash
docker build -t my-app:v1 .
```

---

# Tag Docker Image

```bash
docker tag my-app:v1 username/my-app:v1
```

---

# Run Docker Container

```bash
docker run -d -p 8080:80 nginx
```

---

# List Running Containers

```bash
docker ps
```

---

# List All Containers

```bash
docker ps -a
```

---

# Stop Container

```bash
docker stop <container-id>
```

---

# Remove Container

```bash
docker rm <container-id>
```

---

# Remove Image

```bash
docker rmi my-app:v1
```

---

# View Container Logs

```bash
docker logs <container-id>
```

---

# Execute Commands Inside Container

```bash
docker exec -it <container-id> bash
```

---

# Docker Login

```bash
docker login
```

---

# Push Image to Docker Hub

```bash
docker push username/my-app:v1
```

---

# Pull Image from Docker Hub

```bash
docker pull username/my-app:v1
```

---

# Jenkins Pipeline - Build Docker Image

```groovy
pipeline {

    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app:v1 .'
            }
        }

    }

}
```

Windows

```groovy
pipeline {

    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-app:v1 .'
            }
        }

    }

}
```

---

# Jenkins Pipeline - Push Docker Image

```groovy
pipeline {

    agent any

    stages {

        stage('Push Image') {
            steps {
                sh 'docker push username/my-app:v1'
            }
        }

    }

}
```

---

# Jenkins Pipeline - Run Docker Container

```groovy
pipeline {

    agent any

    stages {

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:80 my-app:v1'
            }
        }

    }

}
```

---

# Archive Build Artifacts

```groovy
archiveArtifacts artifacts: '**/*.jar'
```

---

# Clean Workspace

```groovy
cleanWs()
```

---

# Display Docker Images

```bash
docker images
```

---

# Display Running Containers

```bash
docker ps
```

---

# Remove Unused Docker Resources

```bash
docker system prune -f
```

---

# Git Commands

Stage changes

```bash
git add .
```

Commit changes

```bash
git commit -m "Add Docker integration"
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

# Summary

| Command / Directive | Purpose |
|---------------------|---------|
| `docker build` | Build Docker image |
| `docker run` | Start a container |
| `docker ps` | List running containers |
| `docker images` | List Docker images |
| `docker push` | Push image to Docker Hub |
| `docker pull` | Pull image from registry |
| `docker exec` | Execute command inside container |
| `docker logs` | View container logs |
| `docker system prune` | Remove unused Docker resources |
| `cleanWs()` | Clean Jenkins workspace |

---

# Notes

- Ensure Docker is installed and running before integrating it with Jenkins.
- Add the Jenkins user to the Docker group on Linux to avoid permission issues.
- Use meaningful image names and version tags.
- Push images to a registry such as Docker Hub after successful builds.
- Clean unused Docker resources regularly to save disk space.
- Store Docker Hub credentials securely using Jenkins Credentials.
- Avoid using the `latest` tag for production deployments.