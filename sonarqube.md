# SonarQube Production-Level Hands-On Practice Project (MLOps)

## Objective

Learn how to integrate **SonarQube** into a production-ready MLOps pipeline for continuous code quality, security, and maintainability analysis.

In this hands-on project, you will build an enterprise-grade DevSecOps workflow to analyze:

- Python Source Code
- FastAPI Applications
- Dockerfiles
- Kubernetes Manifests
- Configuration Files
- Unit Test Coverage
- Code Smells
- Bugs
- Security Hotspots
- Vulnerabilities
- Technical Debt

By the end of this project, you'll understand how SonarQube is used in enterprise MLOps CI/CD pipelines before Docker image creation and deployment.

---

# Tech Stack

- Ubuntu
- SonarQube Community Edition
- PostgreSQL
- Docker
- Docker Compose
- Python
- FastAPI
- Git
- GitHub
- SonarScanner
- Java 17

---

# Production Architecture

```text
Developer
      │
      ▼
GitHub
      │
      ▼
SonarScanner
      │
      ▼
SonarQube
      │
      ├── Bugs
      ├── Vulnerabilities
      ├── Code Smells
      ├── Security Hotspots
      ├── Technical Debt
      └── Coverage
      │
      ▼
Quality Gate
      │
      ▼
Docker Build
      │
      ▼
Container Registry
      │
      ▼
Kubernetes
```

---

# Project Structure

```text
sonarqube-mlops-lab/
│
├── app/
│   ├── app.py
│   ├── model.py
│   ├── utils.py
│   ├── requirements.txt
│   └── tests/
│       └── test_app.py
│
├── kubernetes/
│   ├── deployment.yaml
│   └── service.yaml
│
├── Dockerfile
├── docker-compose.yml
├── sonar-project.properties
├── README.md
└── .gitignore
```

---

# Step 1: Install Docker

```bash
sudo apt update

sudo apt install docker.io docker-compose -y

sudo systemctl enable docker

sudo systemctl start docker
```

Verify

```bash
docker --version

docker-compose --version
```

---

# Step 2: Create Project

```bash
mkdir sonarqube-mlops-lab

cd sonarqube-mlops-lab
```

---

# Step 3: Start SonarQube

## docker-compose.yml

```yaml
version: "3.9"

services:

  sonarqube:

    image: sonarqube:lts-community

    container_name: sonarqube

    ports:
      - "9000:9000"

    environment:
      SONAR_ES_BOOTSTRAP_CHECKS_DISABLE: "true"

    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_logs:/opt/sonarqube/logs
      - sonarqube_extensions:/opt/sonarqube/extensions

volumes:

  sonarqube_data:

  sonarqube_logs:

  sonarqube_extensions:
```

Run

```bash
docker-compose up -d
```

Verify

```bash
docker ps
```

---

# Step 4: Access SonarQube

Open

```text
http://localhost:9000
```

Default Login

```text
Username : admin

Password : admin
```

Change password after first login.

---

# Step 5: Install Java

```bash
sudo apt install openjdk-17-jdk -y

java -version
```

---

# Step 6: Install SonarScanner

```bash
sudo snap install sonar-scanner --classic
```

Verify

```bash
sonar-scanner --version
```

---

# Step 7: Create Python Application

## app/app.py

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():

    return {
        "status":"healthy"
    }
```

---

# Step 8: Create Sonar Configuration

## sonar-project.properties

```properties
sonar.projectKey=mlops-sonarqube

sonar.projectName=MLOps SonarQube Demo

sonar.projectVersion=1.0

sonar.sources=app

sonar.language=py

sonar.sourceEncoding=UTF-8
```

---

# Step 9: Generate Authentication Token

SonarQube

```
Administration

↓

Security

↓

Users

↓

Generate Token
```

Copy token.

---

# Step 10: Run SonarScanner

```bash
sonar-scanner \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=YOUR_TOKEN
```

---

# Step 11: View Dashboard

Dashboard displays

- Bugs
- Vulnerabilities
- Code Smells
- Duplicated Code
- Maintainability
- Reliability
- Security Rating
- Technical Debt
- Coverage

---

# Step 12: Create Bad Code

```python
password="admin"

api_key="123456"

print(password)

print(api_key)
```

Run

```bash
sonar-scanner \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=YOUR_TOKEN
```

Observe

- Code Smells
- Security Hotspots

---

# Step 13: Fix Code

Remove hardcoded values.

Use

```python
import os

password = os.getenv("PASSWORD")
```

Scan again.

---

# Step 14: Analyze Dockerfile

```dockerfile
FROM python:latest
```

SonarQube detects

- Latest tag usage
- Best practice violations

---

# Step 15: Analyze Kubernetes Manifests

Example

```yaml
containers:

- image: app:latest
```

SonarQube flags

- latest tag
- Missing resource limits
- Missing security context

---

# Step 16: Generate Test Coverage

Install

```bash
pip install pytest

pip install pytest-cov
```

Run

```bash
pytest \
--cov=app \
tests/
```

Scan again

Coverage appears inside SonarQube.

---

# Step 17: Quality Gate

Configure

```text
Coverage > 80%

Critical Bugs = 0

Security Rating = A

Maintainability = A
```

---

# Step 18: API Testing

Start application

```bash
uvicorn app.app:app \
--host 0.0.0.0 \
--port 8000
```

Health Check

```bash
curl http://localhost:8000
```

Expected

```json
{
  "status":"healthy"
}
```

---

# Step 19: Docker Build

```bash
docker build -t sonarqube-demo .
```

---

# Step 20: Production Workflow

```bash
sonar-scanner

docker build

docker push
```

---

# Production Best Practices

## Analyze

```text
Python

Dockerfile

Kubernetes

YAML

Terraform

Helm

Secrets

Coverage

Security
```

---

## Quality Gates

```text
Coverage > 80%

Critical Bugs = 0

Blocker Issues = 0

Security Rating = A

Reliability Rating = A

Maintainability Rating = A
```

---

## Enterprise CI/CD Pipeline

```text
Developer
      │
      ▼
GitHub
      │
      ▼
GitHub Actions
      │
      ▼
Gitleaks
      │
      ▼
Trivy
      │
      ▼
SonarQube
      │
      ▼
Quality Gate
      │
      ▼
Docker Build
      │
      ▼
Container Registry
      │
      ▼
Kubernetes
```

---

# Skills Covered

- SonarQube Installation
- SonarScanner
- Static Code Analysis
- Code Smells
- Security Hotspots
- Bugs
- Vulnerabilities
- Test Coverage
- Technical Debt
- Quality Gates
- DevSecOps
- MLOps Security

---

# Enterprise MLOps DevSecOps Workflow

```text
Developer
      │
      ▼
GitHub
      │
      ▼
Gitleaks
      │
      ▼
Trivy
      │
      ▼
SonarQube
      │
      ▼
Docker
      │
      ▼
AWS ECR
      │
      ▼
Kubernetes
      │
      ▼
Prometheus
      │
      ▼
Grafana
```

---

# Real-World Learning Outcomes

- Perform enterprise-grade static code analysis
- Configure and enforce Quality Gates
- Detect bugs and security vulnerabilities
- Measure test coverage and technical debt
- Integrate SonarQube into MLOps CI/CD pipelines
- Improve code quality before containerization and deployment

---

# Suggested Repository Names

```text
sonarqube-mlops-lab

enterprise-sonarqube-devsecops

sonarqube-code-quality-platform

enterprise-code-quality

mlops-code-quality-platform

devsecops-quality-gates

production-sonarqube-platform
```

## Recommended Repository

```text
enterprise-sonarqube-devsecops
```
