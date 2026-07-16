# Commands

This section contains the commands required to install and verify Jenkins, configure Docker for Jenkins, and manage Jenkins services on different operating systems.

---

# Check Java Installation

Jenkins requires Java to run.

```bash
java --version
```

or

```bash
java -version
```

Example Output:

```text
openjdk 21.0.2
```

---

# Install Jenkins (Ubuntu/Debian)

Update package index:

```bash
sudo apt update
```

Install Java:

```bash
sudo apt install openjdk-21-jdk -y
```

Verify Java:

```bash
java --version
```

Download Jenkins GPG key:

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

Add Jenkins repository:

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

Update package list:

```bash
sudo apt update
```

Install Jenkins:

```bash
sudo apt install jenkins -y
```

---

# Start Jenkins

```bash
sudo systemctl start jenkins
```

---

# Enable Jenkins at Boot

```bash
sudo systemctl enable jenkins
```

---

# Check Jenkins Status

```bash
sudo systemctl status jenkins
```

---

# Restart Jenkins

```bash
sudo systemctl restart jenkins
```

---

# Stop Jenkins

```bash
sudo systemctl stop jenkins
```

---

# View Jenkins Logs

```bash
sudo journalctl -u jenkins
```

Live logs:

```bash
sudo journalctl -u jenkins -f
```

---

# Get Initial Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

# Install Docker

Docker is commonly used with Jenkins to build images, run containers, and deploy applications.

Update package index:

```bash
sudo apt update
```

Install Docker:

```bash
sudo apt install docker.io -y
```

Start Docker:

```bash
sudo systemctl start docker
```

Enable Docker at boot:

```bash
sudo systemctl enable docker
```

Verify Docker installation:

```bash
docker --version
```

Check Docker status:

```bash
sudo systemctl status docker
```

---

# Give Jenkins Permission to Use Docker

Jenkins pipelines run using the `jenkins` Linux user.

Add Jenkins to the Docker group:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins so the new group permissions take effect:

```bash
sudo systemctl restart jenkins
```

Verify Jenkins groups:

```bash
groups jenkins
```

Test Docker access as the Jenkins user:

```bash
sudo -u jenkins docker ps
```

Check whether Jenkins can find Docker:

```bash
sudo -u jenkins which docker
```

Check Docker version as Jenkins:

```bash
sudo -u jenkins docker --version
```

---

# Install Docker Compose

Docker Compose is useful for running multi-container applications, such as an application and a database.

For Ubuntu 24.04:

```bash
sudo apt update
```

Install Docker Compose V2:

```bash
sudo apt install docker-compose-v2 -y
```

Verify Docker Compose:

```bash
docker compose version
```

Test Docker Compose as Jenkins:

```bash
sudo -u jenkins docker compose version
```

---

# Docker Verification

Check Docker version:

```bash
docker --version
```

Find Docker installation path:

```bash
which docker
```

List Docker images:

```bash
docker images
```

List running containers:

```bash
docker ps
```

Test Docker as Jenkins:

```bash
sudo -u jenkins docker ps
```

---

# Open Jenkins Dashboard

Local machine:

```text
http://localhost:8080
```

Remote server:

```text
http://<server-ip>:8080
```

---

# Firewall (Ubuntu)

Allow Jenkins port:

```bash
sudo ufw allow 8080
```

Enable firewall:

```bash
sudo ufw enable
```

Check firewall status:

```bash
sudo ufw status
```

---

# Windows

Verify Java:

```powershell
java --version
```

Check Jenkins service:

```powershell
Get-Service Jenkins
```

Start Jenkins:

```powershell
Start-Service Jenkins
```

Stop Jenkins:

```powershell
Stop-Service Jenkins
```

Restart Jenkins:

```powershell
Restart-Service Jenkins
```

---

# Jenkins with Docker

Pull Jenkins image:

```bash
docker pull jenkins/jenkins:lts
```

Run Jenkins:

```bash
docker run -d \
--name jenkins \
-p 8080:8080 \
-p 50000:50000 \
jenkins/jenkins:lts
```

View Jenkins container logs:

```bash
docker logs jenkins
```

Get Jenkins initial administrator password:

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

---

# Docker Commands Used with Jenkins

Build a Docker image:

```bash
docker build -t my-app .
```

Run a Docker container:

```bash
docker run -d -p 8080:8080 my-app
```

List running containers:

```bash
docker ps
```

List all containers:

```bash
docker ps -a
```

Stop a container:

```bash
docker stop <container-id>
```

Remove a container:

```bash
docker rm <container-id>
```

List Docker images:

```bash
docker images
```

Remove a Docker image:

```bash
docker rmi <image-name>
```

---

# Docker Compose Commands

Start services:

```bash
docker compose up -d
```

Build and start services:

```bash
docker compose up -d --build
```

Stop services:

```bash
docker compose down
```

Check running services:

```bash
docker compose ps
```

View service logs:

```bash
docker compose logs
```

Follow live service logs:

```bash
docker compose logs -f
```

Validate a Compose file:

```bash
docker compose config
```

---

# Verify Installation

Check Jenkins:

```bash
sudo systemctl status jenkins
```

Check Docker:

```bash
sudo systemctl status docker
```

Check Docker access as Jenkins:

```bash
sudo -u jenkins docker ps
```

Check Docker Compose:

```bash
docker compose version
```

If all required services are working, the Jenkins and Docker environment is ready for pipeline development.

---

# Summary

| Command | Purpose |
|----------|---------|
| `java --version` | Verify Java installation |
| `sudo apt install jenkins` | Install Jenkins |
| `systemctl start jenkins` | Start Jenkins |
| `systemctl enable jenkins` | Enable Jenkins at boot |
| `systemctl status jenkins` | Check Jenkins status |
| `systemctl restart jenkins` | Restart Jenkins |
| `journalctl -u jenkins` | View Jenkins logs |
| `cat initialAdminPassword` | Get Jenkins unlock password |
| `ufw allow 8080` | Open Jenkins port |
| `sudo apt install docker.io` | Install Docker |
| `systemctl status docker` | Check Docker status |
| `usermod -aG docker jenkins` | Give Jenkins Docker access |
| `sudo -u jenkins docker ps` | Test Docker access as Jenkins |
| `docker-compose-v2` | Install Docker Compose V2 |
| `docker compose version` | Verify Docker Compose |
| `docker build` | Build a Docker image |
| `docker run` | Run a Docker container |
| `docker compose up -d` | Start Compose services |
| `docker compose down` | Stop Compose services |
| `docker pull jenkins/jenkins:lts` | Download Jenkins Docker image |