# Commands

This section contains commonly used commands and Jenkins Pipeline snippets for deploying applications to remote servers.

---

# Verify SSH Installation

Linux/macOS

```bash
ssh -V
```

Windows (PowerShell)

```powershell
ssh
```

---

# Generate SSH Key Pair

```bash
ssh-keygen -t rsa -b 4096
```

---

# Copy Public Key to Remote Server

```bash
ssh-copy-id user@server-ip
```

---

# Connect to Remote Server

```bash
ssh user@server-ip
```

---

# Verify Remote Server

```bash
hostname
```

---

# Check Current Directory

```bash
pwd
```

---

# List Files

```bash
ls -la
```

---

# Create Deployment Directory

```bash
mkdir -p /opt/my-app
```

---

# Copy Application to Server

Using SCP:

```bash
scp target/my-app.jar user@server-ip:/opt/my-app/
```

Copy a Docker Compose file:

```bash
scp docker-compose.yml user@server-ip:/opt/my-app/
```

---

# Copy Entire Project

```bash
scp -r project/ user@server-ip:/opt/
```

---

# Restart Application (Systemd)

```bash
sudo systemctl restart my-app
```

---

# Check Application Status

```bash
sudo systemctl status my-app
```

---

# View Application Logs

```bash
journalctl -u my-app -f
```

---

# Docker Deployment

Pull Image

```bash
docker pull username/my-app:v1
```

Run Container

```bash
docker run -d --name my-app -p 8080:8080 username/my-app:v1
```

Stop Container

```bash
docker stop my-app
```

Remove Container

```bash
docker rm my-app
```

Restart Container

```bash
docker restart my-app
```

---

# Deploy Using Docker Compose

```bash
docker compose up -d
```

Stop Services

```bash
docker compose down
```

---

# Jenkins Pipeline - Deploy via SSH

```groovy
pipeline {

    agent any

    stages {

        stage('Deploy') {

            steps {

                sh '''
                scp target/my-app.jar user@server-ip:/opt/my-app/
                ssh user@server-ip "sudo systemctl restart my-app"
                '''

            }

        }

    }

}
```

---

# Jenkins Pipeline - Docker Deployment

```groovy
stage('Deploy Docker') {

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
```

---

# Verify Deployment

Check running application:

```bash
curl http://server-ip:8080
```

---

# Check Open Ports

Linux

```bash
ss -tuln
```

or

```bash
netstat -tuln
```

---

# Check Firewall (Ubuntu)

```bash
sudo ufw status
```

Allow HTTP:

```bash
sudo ufw allow 8080
```

---

# Restart SSH Service

Ubuntu

```bash
sudo systemctl restart ssh
```

CentOS/RHEL

```bash
sudo systemctl restart sshd
```

---

# Git Commands

Stage changes

```bash
git add .
```

Commit changes

```bash
git commit -m "Add deployment stage"
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
| `ssh` | Connect to remote server |
| `scp` | Securely copy files |
| `ssh-copy-id` | Install SSH public key |
| `systemctl restart` | Restart application service |
| `journalctl` | View application logs |
| `docker pull` | Download Docker image |
| `docker run` | Start Docker container |
| `docker compose up -d` | Deploy multi-container application |
| `curl` | Verify deployment |
| `ss -tuln` | Check listening ports |

---

# Notes

- Configure SSH key-based authentication for passwordless deployments.
- Store SSH private keys securely using Jenkins Credentials.
- Verify application health after every deployment.
- Use Docker containers for consistent deployments across environments.
- Keep deployment scripts idempotent so they can be safely executed multiple times.
- Monitor application logs after deployment to detect issues early.
- Test deployments in a staging environment before deploying to production.