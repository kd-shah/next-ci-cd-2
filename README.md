# Docker CI/CD with GitHub Actions (Multi-Environment)

## 📌 Objective
The objective of this assignment is to design and implement a **single GitHub Actions workflow** that builds a Docker image for an application, tags it based on the target environment, and pushes it to **Docker Hub**.  
The workflow supports **development, staging, and production** environments using branch-based triggers.

---

## 🗂 Project Overview
- **Project Type:** Open-source Node.js / Next.js application
- **Containerization:** Docker (multi-stage build)
- **CI/CD Tool:** GitHub Actions
- **Container Registry:** Docker Hub

The same Dockerfile is reused across all environments, ensuring consistency and avoiding duplication.

---

## 🔧 Workflow Design

The GitHub Actions workflow is structured into **three independent jobs**, each corresponding to a specific environment.

### Jobs Overview

| Job Name | Branch Trigger | Docker Tag |
|--------|---------------|-----------|
| dev | `dev` | `:dev` |
| staging | `staging` | `:staging` |
| production | `master` | `:production` |

Each job performs the following steps:
1. Checks out the source code  
2. Logs in to Docker Hub using GitHub Secrets  
3. Builds the Docker image  
4. Tags the image based on the environment  
5. Pushes the image to Docker Hub  

---

## 🚀 Branch-Based Execution Logic

The workflow ensures **only one job runs per branch** using conditional execution:

- Push to `dev` → **only dev job runs**
- Push to `staging` → **only staging job runs**
- Push to `master` → **only production job runs**

This guarantees strict environment isolation and prevents accidental deployments.

---

## 🔐 Environment Variables & Secrets

To follow security best practices:

- No credentials or sensitive values are hardcoded
- All secrets are managed via **GitHub Repository Secrets**

### Required Secrets

| Secret Name | Description |
|-----------|-------------|
| `DOCKER_USERNAME` | Docker Hub username |
| `DOCKER_PASSWORD` | Docker Hub access token |
| `IMAGE_NAME` | Docker image name (e.g. `username/app-name`) |

Secrets are securely injected into the workflow at runtime.

---

## 🐳 Docker Implementation

- Multi-stage Dockerfile is used to optimize image size
- Production-ready build using **Next.js standalone output**
- Environment-specific configuration is handled via build arguments and runtime variables

The same Dockerfile is reused across all environments.

---

## 🔄 Docker Hub Integration

- Docker Hub login is performed using GitHub Secrets
- Authentication happens before build and push steps
- Images are pushed with environment-specific tags

---

## ✅ Assignment Requirements Mapping

| Requirement | Status |
|------------|--------|
| Single GitHub Actions workflow | ✅ |
| Three jobs (dev, staging, production) | ✅ |
| Docker image build per environment | ✅ |
| No hardcoded secrets | ✅ |
| Branch-based triggers | ✅ |
| Docker Hub authentication via secrets | ✅ |

---

## 🏁 Conclusion

This project implements a **production-ready CI/CD pipeline** using GitHub Actions and Docker.  
All assignment objectives have been **successfully completed**, following industry best practices for security, scalability, and maintainability.

