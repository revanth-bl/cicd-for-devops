# Episode 08 - GitHub Webhooks

## Overview

GitHub Webhooks enable **event-driven automation** by allowing GitHub to notify Jenkins whenever specific repository events occur. Instead of Jenkins repeatedly checking for changes, GitHub sends an HTTP POST request immediately after an event such as a code push.

This mechanism is the foundation of modern **Continuous Integration (CI)** because it automatically starts builds, tests, and deployments without manual intervention.

In this chapter, you'll learn how GitHub Webhooks work, configure them with Jenkins, understand webhook events, and build an automated CI workflow.

---

# Learning Objectives

After completing this chapter, you will be able to:

- Understand GitHub Webhooks
- Configure GitHub Webhooks with Jenkins
- Enable automatic builds after Git pushes
- Understand webhook events
- Verify webhook deliveries
- Troubleshoot common webhook issues
- Compare Webhooks with Poll SCM

---

# What is a GitHub Webhook?

A GitHub Webhook is an HTTP callback that sends repository event information to another application.

Whenever a selected event occurs, GitHub sends a JSON payload to a configured URL.

For Jenkins, this means every code push can automatically trigger a build.

---

# Why Use GitHub Webhooks?

Without Webhooks:

```text
Developer
     │
     ▼
Push Code
     │
     ▼
Jenkins Polls Repository
     │
     ▼
Eventually Detects Changes
     │
     ▼
Build Starts
```

Problems:

- Delayed builds
- Unnecessary polling
- Increased server load

---

With Webhooks:

```text
Developer
     │
     ▼
Push Code
     │
     ▼
GitHub
     │
HTTP POST
     │
     ▼
Jenkins
     │
     ▼
Pipeline Starts Immediately
```

Benefits:

- Faster feedback
- Lower server load
- Real-time automation

---

# How GitHub Webhooks Work

```text
Developer
     │
     ▼
Git Commit
     │
     ▼
Git Push
     │
     ▼
GitHub Repository
     │
     ▼
Webhook Triggered
     │
HTTP POST Request
     │
     ▼
Jenkins
     │
     ▼
Pipeline Executes
     │
     ▼
Build
     │
     ▼
Test
     │
     ▼
Deploy
```

---

# Webhook Components

A GitHub Webhook contains the following configuration:

- Payload URL
- Content Type
- Secret
- Events
- Active Status

Each option determines how GitHub communicates with Jenkins.

---

# Payload URL

The Payload URL is the endpoint that receives webhook events.

Example:

```text
http://your-server:8080/github-webhook/
```

For local Jenkins installations, a public tunnel (such as ngrok) is required because GitHub cannot access `localhost`.

---

# Content Type

GitHub supports:

```text
application/json
```

and

```text
application/x-www-form-urlencoded
```

For Jenkins, **application/json** is recommended.

---

# Secret

A webhook secret allows Jenkins to verify that requests originate from GitHub.

Benefits include:

- Request validation
- Improved security
- Protection against unauthorized requests

---

# Events

GitHub can trigger webhooks for many repository events.

Common events include:

- Push
- Pull Request
- Release
- Tag Creation
- Branch Creation
- Issue Events

For Continuous Integration, select:

```text
Just the push event
```

---

# Configuring Jenkins

Inside your Jenkins job:

```
Configure
      ↓
Build Triggers
      ↓
GitHub hook trigger for GITScm polling
```

Enable this option to allow Jenkins to respond to incoming webhook events.

---

# Configuring GitHub

Navigate to:

```
Repository
      ↓
Settings
      ↓
Webhooks
      ↓
Add Webhook
```

Configure:

Payload URL

```text
http://your-server:8080/github-webhook/
```

Content Type

```text
application/json
```

Secret

```text
(Optional but Recommended)
```

Events

```text
Just the push event
```

Save the webhook.

---

# Testing a Webhook

After pushing code:

```bash
git add .
git commit -m "Test webhook"
git push origin main
```

GitHub sends an HTTP POST request to Jenkins.

Verify the delivery:

```
Repository
      ↓
Settings
      ↓
Webhooks
      ↓
Recent Deliveries
```

Successful requests return:

```text
HTTP 200 OK
```

---

# Webhook Delivery Flow

```text
Push Code
     │
     ▼
GitHub Creates Event
     │
     ▼
HTTP POST Request
     │
     ▼
Jenkins Receives Payload
     │
     ▼
Pipeline Starts
     │
     ▼
Console Output
```

---

# GitHub Webhook vs Poll SCM

| Feature | GitHub Webhook | Poll SCM |
|----------|----------------|-----------|
| Trigger | Event Driven | Scheduled Polling |
| Build Start | Immediate | Delayed |
| Network Usage | Low | Higher |
| Efficiency | High | Moderate |
| Recommended | Yes | Only if Webhooks are unavailable |

---

# HTTP Response Codes

| Status | Meaning |
|----------|---------|
| 200 OK | Success |
| 301 / 302 | Redirect |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Endpoint Not Found |
| 500 | Jenkins Internal Error |

---

# Security Best Practices

- Use HTTPS whenever possible.
- Configure a webhook secret.
- Trigger only required events.
- Restrict Jenkins administrator access.
- Keep Jenkins plugins updated.
- Monitor webhook deliveries regularly.

---

# Advantages

- Event-driven automation
- Faster Continuous Integration
- Reduced polling
- Lower server load
- Immediate build execution
- Easy GitHub integration
- Production-ready workflow

---

# Common Mistakes

- Incorrect Payload URL
- Missing `/github-webhook/` endpoint
- Webhook not marked as Active
- Build trigger disabled in Jenkins
- Firewall blocking incoming requests
- Jenkins not publicly accessible
- Incorrect repository permissions

---

# Best Practices

- Use GitHub Webhooks instead of Poll SCM whenever possible.
- Protect webhook endpoints with HTTPS and a secret.
- Keep webhook events limited to those required.
- Verify webhook deliveries after configuration.
- Regularly review Jenkins Console Output and webhook logs.

---

# Key Takeaways

- GitHub Webhooks enable **real-time Continuous Integration** by notifying Jenkins whenever repository events occur.
- Jenkins automatically starts builds after receiving webhook events.
- Webhooks are more efficient than Poll SCM because they eliminate unnecessary polling.
- Secure webhook communication using HTTPS and webhook secrets.
- Proper webhook configuration is essential for reliable CI/CD automation.

---

# References

- Jenkins Official Documentation
- GitHub Webhooks Documentation
- Jenkins GitHub Plugin Documentation

---

# Next Topic

➡️ **Episode 09 – Jenkins Credentials**

In the next chapter, you'll learn how to securely store and manage sensitive information such as GitHub Personal Access Tokens (PATs), SSH keys, usernames, passwords, API keys, and cloud credentials using **Jenkins Credentials**, eliminating the need to hardcode secrets in your pipelines.