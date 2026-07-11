# Troubleshooting

This guide covers common issues encountered while integrating Docker with Jenkins in a CI/CD pipeline.

---

# 1. Docker Command Not Found

## Problem

```text
docker: command not found
```

or

```text
'docker' is not recognized as an internal or external command
```

## Cause

Docker is not installed or its executable is not available in the system PATH.

## Solution

Verify Docker installation:

```bash
docker --version
```

Install Docker Desktop (Windows/macOS) or Docker Engine (Linux), then restart the terminal.

---

# 2. Docker Daemon Not Running

## Problem

```text
Cannot connect to the Docker daemon
```

## Cause

The Docker service is stopped.

## Solution

Linux:

```bash
sudo systemctl start docker
```

Check status:

```bash
sudo systemctl status docker
```

Windows:

Start Docker Desktop and wait until it reports **Docker Engine Running**.

---

# 3. Permission Denied

## Problem

```text
permission denied while trying to connect to the Docker daemon socket
```

## Cause

The Jenkins user is not part of the Docker group.

## Solution

Add Jenkins to the Docker group:

```bash
sudo usermod -aG docker jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Verify:

```bash
groups jenkins
```

---

# 4. Docker Build Failed

## Problem

```text
docker build
```

returns an error.

## Possible Causes

- Invalid Dockerfile
- Missing files
- Incorrect build context
- Syntax errors

## Solution

Verify the Dockerfile:

```bash
docker build -t my-app:v1 .
```

Review the build logs and fix any reported errors.

---

# 5. Docker Image Not Found

## Problem

```text
Unable to find image
```

## Cause

The image has not been built or pulled.

## Solution

List available images:

```bash
docker images
```

If necessary, pull the image:

```bash
docker pull nginx
```

---

# 6. Container Failed to Start

## Problem

```text
Exited (1)
```

## Possible Causes

- Incorrect startup command
- Missing environment variables
- Application crash
- Port conflicts

## Solution

Inspect container logs:

```bash
docker logs <container-id>
```

Correct the configuration and restart the container.

---

# 7. Port Already in Use

## Problem

```text
Bind for 0.0.0.0:8080 failed
```

## Cause

Another application is already using the requested port.

## Solution

Check running containers:

```bash
docker ps
```

Stop the conflicting container:

```bash
docker stop <container-id>
```

Or use another port:

```bash
docker run -p 8081:80 my-app:v1
```

---

# 8. Docker Push Failed

## Problem

```text
denied: requested access to the resource is denied
```

## Cause

- Not logged in
- Incorrect repository name
- Missing permissions

## Solution

Login:

```bash
docker login
```

Verify the image tag:

```bash
docker tag my-app:v1 username/my-app:v1
```

Push again:

```bash
docker push username/my-app:v1
```

---

# 9. Authentication Failed

## Problem

```text
unauthorized: authentication required
```

## Solution

Verify:

- Docker Hub credentials
- Jenkins Credentials configuration
- Repository ownership

Use Jenkins Credentials instead of hardcoding usernames and passwords.

---

# 10. Jenkins Cannot Execute Docker Commands

## Problem

```text
docker: permission denied
```

## Solution

Verify that Jenkins has permission to access Docker.

Linux:

```bash
groups jenkins
```

Restart Jenkins after adding it to the Docker group.

---

# 11. Docker Image Is Too Large

## Problem

Large images increase build and deployment time.

## Solution

- Use lightweight base images.
- Remove unnecessary packages.
- Use multi-stage builds.
- Clean temporary files during image creation.

---

# 12. Container Stops Immediately

## Problem

Container exits immediately after starting.

## Cause

The main application process has finished or crashed.

## Solution

Inspect logs:

```bash
docker logs <container-id>
```

Verify the application's startup command in the Dockerfile.

---

# 13. Jenkins Pipeline Failed During Docker Stage

## Problem

The Docker stage fails in the pipeline.

## Solution

Verify:

- Docker is installed.
- Docker service is running.
- Jenkins has Docker permissions.
- Dockerfile exists in the project root.
- Pipeline syntax is correct.

Review Jenkins Console Output for detailed error messages.

---

# 14. Registry Connection Failed

## Problem

Unable to push or pull images.

## Possible Causes

- Network issues
- Registry unavailable
- Firewall restrictions
- Invalid credentials

## Solution

Verify internet connectivity and registry access.

Test manually:

```bash
docker login
docker pull nginx
```

---

# Useful Verification Commands

Verify Docker:

```bash
docker --version
```

View Docker information:

```bash
docker info
```

List images:

```bash
docker images
```

List running containers:

```bash
docker ps
```

List all containers:

```bash
docker ps -a
```

View container logs:

```bash
docker logs <container-id>
```

Check Jenkins service:

```bash
sudo systemctl status jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Check Docker service:

```bash
sudo systemctl status docker
```

Restart Docker:

```bash
sudo systemctl restart docker
```

---

# Best Practices

- Keep Docker Engine updated.
- Use official base images whenever possible.
- Tag images with version numbers instead of `latest`.
- Store registry credentials securely in Jenkins.
- Remove unused images and containers regularly.
- Monitor Jenkins Console Output during Docker builds.
- Scan Docker images for security vulnerabilities.
- Test Docker images locally before using them in CI/CD pipelines.

---

# Summary

Most Docker Integration issues are caused by Docker installation problems, daemon availability, permission errors, authentication failures, incorrect Dockerfiles, or registry connectivity issues. Reviewing **Jenkins Console Output**, **Docker logs**, and verifying Docker, Jenkins, and registry configurations will resolve the majority of Docker-related pipeline problems.