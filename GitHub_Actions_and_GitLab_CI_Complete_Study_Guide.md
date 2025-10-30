
# GitHub Actions & GitLab CI/CD - Complete DevOps Interview & Study Guide

This guide covers everything you need to confidently answer **GitHub Actions**, **GitLab**, and **GitLab CI/CD** interview questions — from basic concepts to advanced automation pipelines with real-world examples.

---

## 🧠 1. What is GitHub Actions?

**Answer:**
GitHub Actions is a **CI/CD platform** built into GitHub that allows you to **automate your build, test, and deployment workflows** directly from your repository.

**Key Features:**
- Built into GitHub — no separate setup needed.  
- Supports **YAML-based workflow definitions**.  
- Triggers on **GitHub events** (push, pull_request, issue, etc.).  
- Runs jobs inside **Docker containers or VMs**.  
- Supports **matrix builds** and **self-hosted runners**.

---

## ⚙️ 2. GitHub Actions Architecture

**Components:**
- **Workflow:** The complete automation process (defined in `.github/workflows/*.yml`).
- **Job:** A group of steps executed on the same runner.
- **Step:** Individual task in a job (run commands or actions).
- **Action:** Reusable commands packaged as YAML or Docker containers.
- **Runner:** Machine that executes the workflow.

---

## 🧩 3. Example GitHub Actions Workflow

```yaml
name: CI Pipeline

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

      - name: Deploy
        if: github.ref == 'refs/heads/main'
        run: echo "Deploying to production..."
```

---

## 🧰 4. Common GitHub Actions Commands

| Task | Command / Description |
|------|------------------------|
| Define workflow file | `.github/workflows/ci.yml` |
| Manually trigger | `workflow_dispatch` |
| Trigger on push | `on: push` |
| Use predefined action | `uses: actions/checkout@v3` |
| Run shell command | `run: echo Hello World` |
| Access secrets | `${{ secrets.SECRET_NAME }}` |
| Conditional step | `if: github.event_name == 'push'` |

---

## 🔑 5. Managing Secrets in GitHub Actions

**Steps:**
1. Go to repo → Settings → Secrets → Actions.  
2. Add a new secret (e.g., `AWS_ACCESS_KEY`).  
3. Use it in workflow:
   ```yaml
   env:
     AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY }}
   ```

---

## ☁️ 6. GitHub Actions with Docker & AWS

**Build and Push Docker Image:**
```yaml
name: Build and Push Docker Image
on: [push]

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Docker image
        run: docker build -t myapp:${{ github.sha }} .
      - name: Push to Docker Hub
        run: |
          echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
          docker push myapp:${{ github.sha }}
```

---

## 🧪 7. Advanced Concepts

**Matrix Builds:**
```yaml
strategy:
  matrix:
    node: [14, 16, 18]
steps:
  - uses: actions/setup-node@v3
    with:
      node-version: ${{ matrix.node }}
```

**Reusable Workflows:**
```yaml
jobs:
  call-reusable:
    uses: user/repo/.github/workflows/deploy.yml@main
```

**Self-hosted Runner:**
- Configure your own machine as a runner:
  ```bash
  ./config.sh --url https://github.com/your/repo --token <token>
  ./run.sh
  ```

---

## 🚀 8. GitHub Actions Interview Questions

**Q1: What are GitHub Actions used for?**  
A: To automate CI/CD workflows, testing, and deployments within GitHub.

**Q2: What is the syntax format of a workflow file?**  
A: YAML (`.yml`) under `.github/workflows/` directory.

**Q3: How can we trigger a GitHub Action manually?**  
A: Use `workflow_dispatch` event.

**Q4: Can we have multiple workflows in one repository?**  
A: Yes, each workflow file can be defined separately under `.github/workflows/`.

**Q5: What are GitHub-hosted vs. self-hosted runners?**  
A: GitHub-hosted are managed by GitHub; self-hosted are user-managed.

**Q6: How do you pass data between jobs?**  
A: Use `outputs` and `needs` keywords.

**Q7: How do you integrate GitHub Actions with AWS?**  
A: Configure AWS credentials using `aws-actions/configure-aws-credentials`.

---

# 🧩 GitLab Overview

## 🧠 1. What is GitLab?

**Answer:**
GitLab is a **web-based DevOps lifecycle tool** that provides a **Git repository manager**, CI/CD pipelines, issue tracking, and DevSecOps capabilities — all in one platform.

**Key Features:**
- Source code management (SCM)  
- Built-in CI/CD pipeline (GitLab CI)  
- Container registry  
- Infrastructure as Code integration  
- Monitoring and analytics  

---

## ⚙️ 2. GitLab Architecture Overview

1. **Git Repository Management** – Version control with Git.  
2. **GitLab Runner** – Executes pipeline jobs.  
3. **GitLab CI/CD** – Automates build, test, deploy.  
4. **Container Registry** – Store Docker images.  
5. **GitLab Pages** – Host static websites.  

---

## 🧩 3. What is GitLab CI/CD?

**Answer:**
GitLab CI/CD is a **continuous integration and deployment system** built into GitLab. Pipelines are defined in a `.gitlab-ci.yml` file located at the root of the repo.

---

## 🧾 4. Example `.gitlab-ci.yml`

```yaml
stages:
  - build
  - test
  - deploy

variables:
  IMAGE_TAG: $CI_REGISTRY_IMAGE:$CI_COMMIT_REF_SLUG

build:
  stage: build
  script:
    - docker build -t $IMAGE_TAG .
    - docker push $IMAGE_TAG

test:
  stage: test
  script:
    - echo "Running tests..."
    - pytest

deploy:
  stage: deploy
  script:
    - echo "Deploying app..."
    - kubectl apply -f k8s/
  only:
    - main
```

---

## 🧰 5. GitLab CI/CD Components

| Component | Description |
|------------|-------------|
| `.gitlab-ci.yml` | Main CI/CD configuration file |
| Job | Defines actions to run |
| Stage | Logical grouping of jobs |
| Runner | Executes the jobs |
| Artifact | File generated during CI/CD process |

---

## ☁️ 6. GitLab Runner

**What is it?**  
A runner is an agent that executes CI/CD jobs.

**Installation (Linux):**
```bash
sudo apt-get install gitlab-runner -y
sudo gitlab-runner register
# Enter GitLab URL and registration token
sudo systemctl start gitlab-runner
```

---

## 🧪 7. Common GitLab CI/CD Interview Questions

**Q1: How does GitLab CI/CD work?**  
A: Pipelines are triggered automatically on commits or manually. GitLab runners then execute jobs defined in `.gitlab-ci.yml`.

**Q2: What is the difference between shared and specific runners?**  
A: Shared runners are available to all projects; specific runners are linked to particular projects.

**Q3: How do you trigger pipelines manually?**  
A: Via GitLab UI → CI/CD → Pipelines → Run Pipeline.

**Q4: How do you pass environment variables?**  
A: Define them in the UI under Settings → CI/CD → Variables or in `.gitlab-ci.yml`.

**Q5: Can GitLab CI be used with Docker?**  
A: Yes, by using the Docker executor.

**Q6: How can GitLab integrate with Kubernetes?**  
A: GitLab provides direct Kubernetes integration for deploying workloads via `kubectl`.

---

## 🧩 8. GitHub Actions vs. GitLab CI/CD

| Feature | GitHub Actions | GitLab CI/CD |
|----------|----------------|---------------|
| Host Platform | GitHub | GitLab |
| Workflow File | `.github/workflows/*.yml` | `.gitlab-ci.yml` |
| Built-in Runner | GitHub-hosted runner | GitLab Runner |
| Container Registry | Needs Docker Hub/AWS | Built-in Container Registry |
| Triggers | GitHub events (push, PR) | Push, Merge, Manual |
| Secrets Management | Repo Settings → Secrets | Settings → CI/CD → Variables |
| Reusable Workflows | Yes | Yes (via templates) |

---

## 🧾 9. Real-world CI/CD Example

**End-to-End CI/CD using GitHub Actions or GitLab:**
1. Developer pushes code to repo.  
2. Workflow triggers automatically.  
3. Build and test jobs run.  
4. Docker image built and pushed.  
5. Deploy to AWS or Kubernetes.

---

## ✅ Final Tips

- Learn how to create CI/CD pipelines using both GitHub and GitLab.  
- Understand differences between **self-hosted runners** and **cloud runners**.  
- Practice building **Dockerized applications** with automated deployment pipelines.  
- Be ready to explain **YAML syntax, triggers, environments, and stages**.

---
