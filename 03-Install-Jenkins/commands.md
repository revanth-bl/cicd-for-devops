# Commands

This section contains the commands required to install and verify Jenkins on different operating systems.

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

Example Output

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

# Open Jenkins Dashboard

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

# Docker (Optional)

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

View logs:

```bash
docker logs jenkins
```

Get admin password:

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

---

# Verify Installation

Open:

```text
http://localhost:8080
```

If the Jenkins dashboard loads successfully, the installation is complete.

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
| `cat initialAdminPassword` | Get unlock password |
| `ufw allow 8080` | Open Jenkins port |
| `docker pull jenkins/jenkins:lts` | Download Jenkins Docker image |