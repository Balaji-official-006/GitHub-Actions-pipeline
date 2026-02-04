# GitHub Actions → EC2 Deployment Project

## Project Title  
Automated CI/CD Pipeline Using GitHub Actions to Deploy Source Code to EC2 (Nginx)

---

## Project Overview

This project demonstrates how to build a simple CI/CD pipeline using GitHub Actions to automatically deploy source code from GitHub to an AWS EC2 instance running Nginx. Whenever code is pushed to the main branch, GitHub Actions triggers a workflow that securely connects to EC2 using SSH, copies the application files, and updates the Nginx web root. This simulates a real-world DevOps deployment workflow without containers.

---

## Architecture Flow

GitHub → GitHub Actions → SCP → SSH → EC2 → Nginx → Browser



---

## Tools Used

- GitHub (Source Code Repository)
- GitHub Actions (CI/CD Automation)
- AWS EC2 (Deployment Server)
- Nginx (Web Server)
- SSH / SCP (Secure Deployment)

---

## Implementation Steps

### 1. EC2 Setup

- Launched EC2 instance
- Installed Nginx
- Configured custom Nginx root directory
- Created deployment folder `/home/ec2-user/app`
- Updated permissions for deployment directories

---

### 2. GitHub Repository Setup

Repository structure:

  .
├── index.html
└── .github/workflows/deploy.yml


---

### 3. GitHub Secrets Configuration

Added repository secrets:

- `EC2_HOST`
- `EC2_USER`
- `EC2_KEY`

These are used by GitHub Actions for secure SSH access.

---

### 4. GitHub Actions Workflow

- Triggered on push to `main` branch
- Checkout source code
- Copy files to EC2 using SCP
- SSH into EC2
- Replace Nginx root content
- Reload Nginx

This enables automatic deployment on every Git push.

---

## Issues Faced & Solutions

• **Workflow not appearing in GitHub Actions**  
→ Ensured workflow file existed inside `.github/workflows` and added `workflow_dispatch`.

• **SSH connected but files not copied**  
→ Replaced SSH-only deployment with SCP + SSH combination.

• **cp: cannot stat '*' error**  
→ Realized code existed only on GitHub runner, not EC2. Fixed by transferring files first using SCP.

• **Nginx page not updating after deployment**  
→ Matched GitHub Actions deployment path with Nginx root directory.

• **Permission denied while copying files**  
→ Updated ownership of Nginx root directory using `chown`.

• **kubectl not relevant for this project**  
→ Simplified deployment to pure EC2 + Nginx.

• **Incorrect folder structure in repository**  
→ Fixed `.github/workflows/deploy.yml` placement.

• **Manual trigger not available**  
→ Added `workflow_dispatch` to enable manual execution.

---

## Final Outcome

- Source code stored in GitHub  
- GitHub Actions automatically triggered on push  
- Files securely transferred to EC2  
- Nginx web root updated  
- Website refreshed automatically  

A fully automated GitHub Actions → EC2 deployment pipeline was achieved.

---

## Key Learnings

- GitHub Actions workflow creation
- Secure EC2 deployment using SSH and SCP
- Nginx document root configuration
- Linux file permissions
- CI/CD automation without containers
- Real-world DevOps troubleshooting

---

## Resume Summary

Built an automated CI/CD pipeline using GitHub Actions to deploy source code directly to AWS EC2 running Nginx. Implemented SSH and SCP-based deployments, handled file permissions, configured custom Nginx root paths, and resolved multiple workflow and deployment issues to achieve continuous delivery from GitHub to EC2.

