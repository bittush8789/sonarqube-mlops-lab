# SonarQube Production-Level Hands-On Practice Project (MLOps)

## Overview

A production-ready **DevSecOps** project demonstrating how to integrate **SonarQube** into an MLOps workflow for continuous code quality, security, and maintainability analysis.

This project analyzes Python applications, Dockerfiles, Kubernetes manifests, and configuration files to identify bugs, vulnerabilities, code smells, security hotspots, and technical debt before deployment.

## Features

* Static Code Analysis
* Bug Detection
* Vulnerability Analysis
* Security Hotspot Detection
* Code Smell Detection
* Technical Debt Analysis
* Test Coverage Reporting
* Quality Gate Validation
* CI/CD Ready Integration

## Tech Stack

* SonarQube
* SonarScanner
* Python
* FastAPI
* Docker
* Docker Compose
* Git & GitHub
* Kubernetes

## Architecture

```text id="7jlwmf"
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
    └── Quality Gate
    │
    ▼
Docker Build
    │
    ▼
Kubernetes
```

## Project Structure

```text id="mxck4m"
enterprise-sonarqube-devsecops/
│
├── app/
├── kubernetes/
├── Dockerfile
├── docker-compose.yml
├── sonar-project.properties
└── README.md
```

## Quick Start

### Clone Repository

```bash id="ihk16i"
git clone https://github.com/<your-username>/enterprise-sonarqube-devsecops.git

cd enterprise-sonarqube-devsecops
```

### Start SonarQube

```bash id="btrtkw"
docker-compose up -d
```

### Run Code Analysis

```bash id="n7rj9d"
sonar-scanner \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=<YOUR_TOKEN>
```

## Access SonarQube

```text id="hq2tvy"
URL      : http://localhost:9000

Username : admin

Password : admin
```

## Test Application

```bash id="9tnsqk"
curl http://localhost:8000
```

Response

```json id="tqgmff"
{
  "status": "healthy"
}
```

## Skills Demonstrated

* SonarQube Installation
* SonarScanner
* Static Code Analysis
* Security Analysis
* Code Quality Management
* Quality Gates
* Test Coverage
* DevSecOps for MLOps

## Enterprise DevSecOps Pipeline

```text id="h6tqns"
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
Docker Build
      │
      ▼
Container Registry
      │
      ▼
Kubernetes
```

## Future Enhancements

* GitHub Actions Integration
* MLflow Integration
* AWS ECR
* Kubernetes Deployment
* Prometheus Monitoring
* Grafana Dashboards

## License

This project is intended for learning and demonstrating production-ready code quality and DevSecOps practices in MLOps.
