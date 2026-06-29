# CI/CD — Practical Overview & Commands

CI/CD (Continuous Integration and Continuous Deployment) automates the building, testing, and delivery of software to production environments.
Its primary goals include:

* Faster release cycles
* Consistent, repeatable deployments
* Reduced manual errors
* Higher developer productivity

---

## 1. Source Control & Repository Setup

| Command / Tool                     | Purpose                          |
| ---------------------------------- | -------------------------------- |
| `git init`                         | Initialize a Git repository      |
| `git add .`                        | Stage all changes                |
| `git commit -m "message"`          | Commit staged changes            |
| `git remote add origin <repo_url>` | Connect local repo to remote     |
| `git push origin main`             | Push commits to main branch      |
| `gh workflow list`                 | Display GitHub Actions workflows |
| `gh workflow run <name>`           | Trigger a workflow manually      |
| `gh run watch`                     | Stream workflow execution logs   |

---

## 2. Continuous Integration (CI)

Continuous Integration focuses on automatic building and testing of code changes before merging into mainline branches.

### Typical CI Pipeline Stages

| Stage                     | Tool / Command                                    | Purpose                            |
| ------------------------- | ------------------------------------------------- | ---------------------------------- |
| Build                     | `docker build -t <image> .`                       | Package or compile the application |
| Dependency Installation   | `npm install` / `pip install -r requirements.txt` | Install dependencies               |
| Automated Testing         | `npm test` / `pytest` / `mvn test`                | Validate correctness               |
| Linting / Static Analysis | `eslint .` / `flake8`                             | Ensure formatting and code quality |
| Artifact Creation         | CI-generated build output                         | Used for deployment                |
| Pipeline Triggers         | `on: [push, pull_request]`                        | Automatically run on commit events |

### Common GitHub Actions CI Components

| Component                                | Purpose                              |
| ---------------------------------------- | ------------------------------------ |
| `actions/checkout@v4`                    | Clone repository source              |
| `actions/setup-node@v4` / `setup-python` | Setup runtime environment            |
| `actions/cache@v4`                       | Cache dependencies for faster builds |

---

## 3. Continuous Deployment (CD)

Continuous Deployment automates delivery of application artifacts to runtime environments like virtual machines, containers, or Kubernetes clusters.

### Deployment Sequence

| Stage             | Command / Tool                             | Purpose                      |
| ----------------- | ------------------------------------------ | ---------------------------- |
| Build Image       | `docker build -t <image> .`                | Build container image        |
| Push Image        | `docker push <repo>/<image>:tag`           | Push to registry             |
| Deploy to K8s     | `kubectl apply -f k8s/`                    | Apply deployment manifests   |
| Verify Deployment | `kubectl get pods` / `kubectl get svc`     | Validate deployment state    |
| Monitor Rollout   | `kubectl rollout status deployment/<name>` | Track deployment progress    |
| Rollback          | `kubectl rollout undo deployment/<name>`   | Revert unsuccessful releases |

### Supported Container Registries

| Registry  | Provider |
| --------- | -------- |
| DockerHub | Docker   |
| ECR       | AWS      |
| GCR       | Google   |
| ACR       | Azure    |

---

## 4. Secrets & Security Considerations

Common secrets required in CI/CD pipelines include:

* Docker credentials
* Kubernetes configuration
* API keys or tokens

These should be stored securely via:

**GitHub → Repository → Settings → Secrets & Variables**

---

## 5. Example: GitHub Actions CI/CD Workflow

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ "main" ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Source Code
        uses: actions/checkout@v4

      - name: Setup Node Environment
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install Dependencies
        run: npm install

      - name: Run Tests
        run: npm test

      - name: Build Docker Image
        run: docker build -t ${{ secrets.DOCKER_USERNAME }}/devops-app:latest .

      - name: Authenticate to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Push Image to Docker Registry
        run: docker push ${{ secrets.DOCKER_USERNAME }}/devops-app:latest

      - name: Deploy to Kubernetes Cluster
        env:
          KUBE_CONFIG_DATA: ${{ secrets.KUBE_CONFIG_DATA }}
        run: |
          echo "$KUBE_CONFIG_DATA" | base64 --decode > $HOME/.kube/config
          kubectl apply -f k8s/
          kubectl rollout status deployment/devops-app
```

---

## 6. Deployment Flow (End-to-End)

```
Commit → CI (Build/Test) → Container Registry → CD → Kubernetes → Service Exposure
```

---
