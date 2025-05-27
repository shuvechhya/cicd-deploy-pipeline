# cicd-deploy-pipeline
# 🚀 GitLab CI/CD: Deploy to Remote Server

This CI/CD pipeline automates deployment of the project to a remote server using SSH and Git.

---

## 📜 Overview

The pipeline:
- Connects to a remote server via SSH.
- Ensures the deployment directory exists.
- Uses a GitLab Personal Access Token (GLPAT) to pull the latest branch from a Git repository.

---

## ⚙️ Required GitLab CI/CD Variables

In your GitLab project, go to **Settings → CI/CD → Variables** and define the following:

| Variable           | Description                                      | Masked | Protected |
|--------------------|--------------------------------------------------|--------|-----------|
| `SSH_PRIVATE_KEY`  | Private SSH key with access to the remote server | ✅     | ✅         |
| `GLPAT`            | GitLab Personal Access Token (read access)       | ✅     | ✅         |
| `CI_GIT_USERNAME`  | Your GitLab username                             | ✅     | ✅         |

---

## 📁 Assumptions About Remote Server

- SSH is available on **port 9022**.
- The target user is `abc` (replace with the actual username).
- The deployment path is `/path/to/deployment/uat_ssp`.
- The server can `git pull` from the repository using a token.

---

## 📝 Pipeline Steps

### 1. SSH Setup
- Adds your private SSH key and converts it to PEM format if needed.

### 2. Remote Preparation
- Ensures the remote deployment folder exists.

### 3. Git Configuration
- Sets global Git identity.
- Stores Git credentials securely using variables.

### 4. Deploy
- Pulls the latest code from the specified branch to the remote directory.

---

## 🔒 Security Notes

- Tokens and SSH keys are **never hardcoded** in this pipeline.
- All sensitive data must be added via **CI/CD Variables**.
- Ensure your GitLab token has **read_repository** permission at minimum.

---

## 📌 Replace Dummy Values

Make sure to replace the following dummy values in `.gitlab-ci.yml` with your actual values:
- `abc@192.0.2.1` → your SSH user and host
- `/path/to/deployment/uat_ssp` → your actual deploy path
- `git.example.com` → your GitLab instance URL
- `your-group/uat_ssp.git` → your actual project path

---

Maintained by your DevOps team.
