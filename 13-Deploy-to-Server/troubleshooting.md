# Troubleshooting

This guide covers common issues encountered while deploying applications from Jenkins to remote servers using SSH, SCP, Docker, and deployment scripts.

---

# 1. SSH Connection Refused

## Problem

```text
ssh: connect to host <server-ip> port 22: Connection refused
```

## Cause

- SSH service is not running
- Incorrect IP address
- Firewall blocking port 22

## Solution

Verify SSH service:

Ubuntu

```bash
sudo systemctl status ssh
```

CentOS/RHEL

```bash
sudo systemctl status sshd
```

Start SSH service if necessary:

Ubuntu

```bash
sudo systemctl start ssh
```

CentOS/RHEL

```bash
sudo systemctl start sshd
```

---

# 2. Permission Denied (Public Key)

## Problem

```text
Permission denied (publickey)
```

## Cause

- Incorrect SSH key
- Public key not installed
- Wrong username

## Solution

Generate an SSH key if required:

```bash
ssh-keygen -t rsa -b 4096
```

Copy the public key:

```bash
ssh-copy-id user@server-ip
```

Test the connection:

```bash
ssh user@server-ip
```

---

# 3. SCP File Transfer Failed

## Problem

```text
scp: No such file or directory
```

## Cause

- Incorrect file path
- Destination directory does not exist

## Solution

Verify the local file:

```bash
ls target/
```

Create the destination directory:

```bash
mkdir -p /opt/my-app
```

Retry the transfer.

---

# 4. Jenkins Cannot Connect to Server

## Problem

Deployment stage fails while establishing an SSH connection.

## Solution

Verify:

- Server IP address
- SSH port
- Firewall rules
- Jenkins SSH credentials
- Network connectivity

Test manually:

```bash
ssh user@server-ip
```

---

# 5. Application Failed to Start

## Problem

Application exits immediately after deployment.

## Possible Causes

- Missing dependencies
- Incorrect configuration
- Port already in use

## Solution

Check service status:

```bash
sudo systemctl status my-app
```

Review logs:

```bash
journalctl -u my-app -f
```

---

# 6. Docker Container Failed

## Problem

Container stops immediately.

## Solution

Inspect logs:

```bash
docker logs my-app
```

Verify the Docker image:

```bash
docker images
```

Restart the container:

```bash
docker restart my-app
```

---

# 7. Docker Image Not Found

## Problem

```text
pull access denied
```

## Cause

- Incorrect image name
- Image not pushed
- Authentication failure

## Solution

Login to Docker Hub:

```bash
docker login
```

Verify the image:

```bash
docker images
```

Pull again:

```bash
docker pull username/my-app:v1
```

---

# 8. Service Not Running

## Problem

```text
Unit my-app.service could not be found.
```

## Cause

The Systemd service has not been created or configured.

## Solution

Verify available services:

```bash
systemctl list-units --type=service
```

Reload Systemd after creating a service:

```bash
sudo systemctl daemon-reload
```

Enable the service:

```bash
sudo systemctl enable my-app
```

---

# 9. Port Already in Use

## Problem

```text
Address already in use
```

## Cause

Another application is using the required port.

## Solution

Check listening ports:

```bash
ss -tuln
```

or

```bash
netstat -tuln
```

Stop the conflicting application or use a different port.

---

# 10. Firewall Blocking Application

## Problem

Application is running but cannot be accessed remotely.

## Solution

Check firewall status:

Ubuntu

```bash
sudo ufw status
```

Allow the application port:

```bash
sudo ufw allow 8080
```

---

# 11. Deployment Verification Failed

## Problem

Application health check fails after deployment.

## Solution

Test manually:

```bash
curl http://server-ip:8080
```

Review application logs:

```bash
journalctl -u my-app -f
```

Verify that the service is active.

---

# 12. Jenkins Credentials Not Found

## Problem

```text
Credentials not found
```

## Solution

Navigate to:

```text
Manage Jenkins
    ↓
Credentials
```

Verify:

- Credential ID
- SSH private key
- Username
- Scope

---

# 13. Docker Compose Deployment Failed

## Problem

```text
docker compose up
```

returns an error.

## Solution

Validate the configuration:

```bash
docker compose config
```

Restart services:

```bash
docker compose down
docker compose up -d
```

---

# 14. Rollback Required

## Problem

The new deployment is unstable.

## Solution

Deploy the previous stable version.

Docker example:

```bash
docker pull username/my-app:v1
docker stop my-app
docker rm my-app
docker run -d --name my-app -p 8080:8080 username/my-app:v1
```

---

# Useful Verification Commands

Check SSH connection:

```bash
ssh user@server-ip
```

Copy a file:

```bash
scp file user@server-ip:/opt/my-app/
```

Verify Docker:

```bash
docker --version
```

List containers:

```bash
docker ps
```

View logs:

```bash
docker logs my-app
```

Check application service:

```bash
sudo systemctl status my-app
```

Restart service:

```bash
sudo systemctl restart my-app
```

View service logs:

```bash
journalctl -u my-app -f
```

Verify open ports:

```bash
ss -tuln
```

Test application:

```bash
curl http://server-ip:8080
```

---

# Best Practices

- Use SSH key authentication instead of passwords.
- Store SSH credentials securely in Jenkins Credentials.
- Test deployments in a staging environment before production.
- Verify application health after every deployment.
- Maintain versioned releases for quick rollbacks.
- Monitor logs after deployment.
- Automate rollback procedures whenever possible.
- Keep deployment scripts idempotent and version-controlled.

---

# Summary

Most deployment issues result from SSH authentication failures, incorrect server configuration, Docker errors, missing credentials, service startup problems, or network connectivity issues. Reviewing **Jenkins Console Output**, **application logs**, **Docker logs**, and **Systemd service status** will resolve the majority of deployment-related problems quickly and effectively.