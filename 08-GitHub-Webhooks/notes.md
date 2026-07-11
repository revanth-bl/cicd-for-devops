# Notes

## What is a GitHub Webhook?

A GitHub Webhook is an HTTP callback that automatically sends event notifications from GitHub to another application, such as Jenkins.

Instead of Jenkins repeatedly checking GitHub for changes, GitHub immediately notifies Jenkins whenever a specified event occurs.

This enables automatic build execution and is a key part of Continuous Integration (CI).

---

# Why Use GitHub Webhooks?

Without Webhooks:

- Jenkins must poll the repository for changes.
- Builds may be delayed.
- Unnecessary network requests are generated.

With Webhooks:

- Builds start immediately after code is pushed.
- Reduced server load.
- Faster feedback for developers.
- More efficient CI/CD workflow.

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
Webhook Event
     │
HTTP POST Request
     │
     ▼
Jenkins
     │
     ▼
Pipeline Triggered
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

# Components of a Webhook

A GitHub Webhook consists of:

- Payload URL
- Content Type
- Secret (optional but recommended)
- Events
- Active status

Each component controls how GitHub communicates with Jenkins.

---

# Payload URL

The Payload URL tells GitHub where to send webhook events.

Example:

```text
http://your-jenkins-server:8080/github-webhook/
```

For local development, use a secure public tunnel such as **ngrok**.

---

# Content Type

GitHub supports two payload formats:

- `application/json` (recommended)
- `application/x-www-form-urlencoded`

Jenkins typically expects **application/json**.

---

# Secret

A webhook secret is a shared value used to verify that requests actually come from GitHub.

Benefits:

- Prevents unauthorized requests.
- Improves security.
- Protects webhook endpoints.

---

# Events

GitHub can trigger webhooks for many repository events.

Common events include:

- Push
- Pull Request
- Branch Creation
- Release Published
- Tag Creation
- Issue Events

For CI, the most common choice is:

```text
Just the push event
```

---

# Jenkins Build Trigger

To respond to webhook events, enable the following option in your Jenkins job:

```text
GitHub hook trigger for GITScm polling
```

This allows Jenkins to start a build whenever GitHub sends a matching webhook event.

---

# Webhook Delivery Process

```text
Git Push
      │
      ▼
GitHub Generates Event
      │
      ▼
HTTP POST Request
      │
      ▼
Jenkins Receives Event
      │
      ▼
Pipeline Starts
      │
      ▼
Console Output
```

---

# HTTP Response Codes

Common webhook responses:

| Status Code | Meaning |
|--------------|---------|
| 200 OK | Webhook processed successfully |
| 301/302 | Redirect |
| 401 Unauthorized | Authentication failed |
| 403 Forbidden | Access denied |
| 404 Not Found | Incorrect webhook URL |
| 500 Internal Server Error | Jenkins server error |

---

# Benefits of Webhooks

- Automatic builds
- Faster feedback
- Reduced polling
- Improved developer productivity
- Real-time CI/CD automation

---

# Common Use Cases

- Trigger Jenkins builds
- Start deployment pipelines
- Run automated tests
- Notify chat applications
- Integrate with monitoring systems

---

# Best Practices

- Use HTTPS whenever possible.
- Configure a webhook secret.
- Trigger only the required events.
- Monitor webhook delivery logs.
- Secure Jenkins with authentication.
- Keep Jenkins plugins updated.
- Validate webhook responses regularly.

---

# Common Problems

- Incorrect Payload URL
- Jenkins not reachable from GitHub
- Firewall blocking requests
- Invalid webhook secret
- Missing GitHub plugin
- Build trigger not enabled
- Repository permissions issues

---

# GitHub Webhook vs Poll SCM

| Feature | GitHub Webhook | Poll SCM |
|----------|----------------|-----------|
| Trigger Method | Event-driven | Scheduled polling |
| Speed | Immediate | Delayed |
| Network Usage | Low | Higher |
| Efficiency | High | Moderate |
| Recommended | Yes | Only when webhooks are unavailable |

---

# Security Considerations

To secure webhook communication:

- Enable HTTPS.
- Use a webhook secret.
- Restrict Jenkins access where appropriate.
- Keep Jenkins and plugins updated.
- Review webhook activity logs.

---

# Interview Questions

### What is a GitHub Webhook?

A GitHub Webhook is an HTTP callback that automatically notifies another application, such as Jenkins, when repository events occur.

---

### Why are GitHub Webhooks preferred over Poll SCM?

Webhooks trigger builds immediately after an event, reducing delays and unnecessary polling, making them more efficient.

---

### What is the purpose of the Payload URL?

The Payload URL is the endpoint where GitHub sends webhook event data.

---

### Why should a webhook secret be configured?

A webhook secret verifies that incoming requests are genuinely from GitHub and helps prevent unauthorized access.

---

### Which GitHub event is commonly used to trigger Jenkins builds?

The **Push** event is the most common trigger for Continuous Integration pipelines.

---

# Key Takeaways

- GitHub Webhooks enable **event-driven Continuous Integration**.
- GitHub sends an HTTP POST request to Jenkins whenever configured repository events occur.
- Webhooks provide faster and more efficient build triggering than Poll SCM.
- Secure webhook communication with HTTPS and a shared secret.
- Proper webhook configuration is essential for reliable, automated CI/CD pipelines.