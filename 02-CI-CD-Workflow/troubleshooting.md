# Troubleshooting

This guide covers common issues encountered during the CI/CD workflow, from writing code to triggering an automated pipeline.

---

# 1. Changes Are Not Detected

## Problem

After modifying files, Git does not show any changes.

## Check

```bash
git status
```

## Possible Causes

- File was not saved.
- Working in the wrong directory.
- File is ignored by `.gitignore`.

## Solution

- Save the file.
- Verify your current directory:

```bash
pwd
```

or on Windows:

```powershell
Get-Location
```

- Check `.gitignore`.

---

# 2. Unable to Commit Changes

## Problem

```text
Author identity unknown
```

## Cause

Git username or email is not configured.

## Solution

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Verify:

```bash
git config --global --list
```

---

# 3. Push Rejected

## Problem

```text
failed to push some refs
```

## Cause

The remote repository contains commits that are not present locally.

## Solution

Fetch the latest changes:

```bash
git pull origin main
```

Resolve any merge conflicts, then push again:

```bash
git push origin main
```

---

# 4. Merge Conflicts

## Problem

Git reports merge conflicts after pulling or merging branches.

## Cause

The same lines of code were modified in different commits.

## Solution

- Open the affected file.
- Resolve the conflict manually.
- Remove Git conflict markers.
- Stage and commit the resolved file.

```bash
git add .
git commit -m "Resolve merge conflicts"
```

---

# 5. Wrong Branch

## Problem

Changes were committed to the wrong branch.

## Check Current Branch

```bash
git branch
```

## Switch Branch

```bash
git checkout main
```

---

# 6. Remote Repository Not Found

## Problem

```text
remote: Repository not found
```

## Possible Causes

- Incorrect repository URL.
- Repository has been deleted.
- No permission to access the repository.

## Check Remote URL

```bash
git remote -v
```

Update if necessary:

```bash
git remote set-url origin <repository-url>
```

---

# 7. Authentication Failed

## Problem

```text
Authentication failed
```

## Cause

GitHub no longer supports password authentication for Git operations over HTTPS.

## Solution

- Use a Personal Access Token (PAT).
- Or configure SSH authentication.

---

# 8. Pipeline Does Not Start

## Possible Causes

- CI/CD tool is not connected to the repository.
- Webhooks are not configured.
- Wrong branch is being monitored.
- Trigger conditions are incorrect.

## Solution

- Verify repository integration.
- Check webhook configuration.
- Confirm the correct branch is selected.
- Review pipeline trigger settings.

---

# 9. Build Fails Immediately

## Possible Causes

- Missing dependencies.
- Incorrect build configuration.
- Compilation errors.
- Missing environment variables.

## Solution

- Review build logs.
- Verify project configuration.
- Install required dependencies.
- Fix compilation errors before pushing.

---

# 10. Tests Fail

## Possible Causes

- Application bug.
- Incorrect test configuration.
- Missing test data.
- Environment mismatch.

## Solution

- Review test reports.
- Fix the failing tests.
- Re-run the pipeline.

---

# 11. Deployment Does Not Occur

## Possible Causes

- Previous stage failed.
- Manual approval required.
- Deployment configuration error.

## Solution

- Review the pipeline logs.
- Ensure all previous stages completed successfully.
- Approve the deployment if required.

---

# Useful Verification Commands

Check repository status:

```bash
git status
```

View commit history:

```bash
git log --oneline
```

Check current branch:

```bash
git branch
```

View configured remotes:

```bash
git remote -v
```

Pull latest changes:

```bash
git pull origin main
```

Push changes:

```bash
git push origin main
```

---

# Best Practices

- Commit frequently with meaningful messages.
- Pull the latest changes before starting new work.
- Keep branches up to date.
- Resolve conflicts immediately.
- Review pipeline logs when failures occur.
- Never ignore failed tests or build errors.

---

# Summary

Most CI/CD workflow issues occur before the build or deployment stage. Using Git correctly, keeping repositories synchronized, and reviewing pipeline logs are essential skills for maintaining reliable software delivery pipelines.