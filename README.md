# ACEest Fitness & Gym — DevOps Assignment 2
## CI/CD Pipeline Implementation

**Student Name:** Patil Kinnari Nilesh Kamini  
**BITS ID:** 2025TM93044  
**Programme:** M.Tech Software Engineering  
**Academic Batch:** 2025–2026

**GitHub Repository:** https://github.com/kinnari0403/ACEest-DevOps-Assignment-2

---

## 1. Project Overview

ACEest Fitness & Gym is a Flask-based web application developed to demonstrate the implementation of DevOps practices through an automated Continuous Integration and Continuous Delivery (CI/CD) pipeline.

This assignment extends the application developed in Assignment 1 by integrating version control, automated testing, Jenkins pipeline automation, Docker containerization, SonarQube static code analysis, and Kubernetes deployment configurations.

The objective is to establish an automated software delivery workflow that improves application quality, consistency, maintainability, and deployment readiness.

## 2. Application Features

The application provides the following functionality:

- Register gym members with unique email addresses.
- Log workouts with duration validation.
- View registered members and recent workout records.
- SQLite database integration for data persistence.
- Health-check endpoint (`/health`) for application monitoring and container validation.

## 3. Technology Stack

| Category | Technology |
|---|---|
| Programming Language | Python |
| Web Framework | Flask |
| Database | SQLite |
| Version Control | Git |
| Source Code Repository | GitHub |
| CI/CD Automation | Jenkins |
| Automated Testing | Pytest |
| Code Quality Analysis | SonarQube |
| Containerization | Docker |
| Container Registry | Docker Hub |
| Container Orchestration | Kubernetes |
| Operating Environment | Rocky Linux |

## 4. Project Structure

```text
ACEest-DevOps-Assignment-2/
│
├── app.py
├── requirements.txt
├── requirements-dev.txt
├── pytest.ini
├── Dockerfile
├── .dockerignore
├── .gitignore
├── Jenkinsfile
├── sonar-project.properties
│
├── tests/
│   └── Application test cases
│
├── kubernetes/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── rolling-update.yaml
│   ├── blue-green.yaml
│   ├── canary.yaml
│   ├── shadow.yaml
│   └── ab-testing.yaml
│
├── .github/
│   └── workflows/
│
├── Screenshots/
│   └── Assignment execution evidence
│
├── 2025TM93044_DevOps Assignment 2 Report.pdf
│
└── README.md
```

## 5. CI/CD Architecture

The project follows an automated delivery workflow:

```text
Developer
    |
    v
Git / GitHub Repository
    |
    v
Jenkins Pipeline
    |
    v
Source Code Checkout
    |
    v
Python Environment Setup
    |
    v
Syntax and Lint Validation
    |
    v
Pytest Execution
    |
    v
Docker Image Build
    |
    v
Docker Hub Image Registry
    |
    v
Kubernetes Deployment Configurations
```

SonarQube is used for static code analysis and code quality evaluation.

## 6. Version Control Using Git and GitHub

Git is used to maintain source code history and GitHub is used as the central repository.

Repository:

https://github.com/kinnari0403/ACEest-DevOps-Assignment-2

Git commands:

```bash
git status
git add .
git commit -m "Update application and DevOps configuration"
git push origin main
```

The project uses the `main` branch for the primary application and DevOps configuration.

## 7. Application Setup and Execution

### Prerequisites

- Python 3
- pip
- Git
- Docker (for container execution)

### Clone the repository

```bash
git clone https://github.com/kinnari0403/ACEest-DevOps-Assignment-2.git

cd ACEest-DevOps-Assignment-2
```

### Create a virtual environment

```bash
python3 -m venv .venv

source .venv/bin/activate
```

### Install dependencies

```bash
python -m pip install --upgrade pip

pip install -r requirements-dev.txt
```

### Run the application

```bash
python app.py
```

Application URL:

http://localhost:5000

Health-check endpoint:

http://localhost:5000/health

Expected health response:

```json
{
  "status": "ok"
}
```

## 8. Automated Testing Using Pytest

Pytest is used to validate application functionality and identify errors before the container build stage.

Execute the tests using:

```bash
pytest -q
```

Additional syntax validation:

```bash
python -m compileall -q app.py tests
```

Lint validation:

```bash
ruff check --select F app.py tests
```

**Execution Result:** Six automated test cases passed during the assignment execution.

## 9. Jenkins CI/CD Pipeline

Jenkins is configured to automate the application build and validation process.

The pipeline is defined in the `Jenkinsfile`.

### Pipeline stages

1. **Checkout:** Retrieves the application source code from GitHub.
2. **Set up Python and dependencies:** Creates a virtual environment and installs dependencies.
3. **Syntax and lint:** Performs Python compilation and Ruff checks.
4. **Pytest:** Executes automated unit tests.
5. **Docker Build:** Builds the application container image.

The Jenkins pipeline was configured using Pipeline Script from SCM, with GitHub as the source repository.

The Jenkins agent requires Python, Git, Docker CLI, and Docker daemon access.

## 10. Docker Containerization

Docker is used to package the Flask application and its dependencies into a portable container image.

### Build the Docker image

```bash
docker build -t aceest-fitness:v1.0 .
```

### Run the container

```bash
docker run -d \
  --name aceest-v1 \
  -p 5000:5000 \
  aceest-fitness:v1.0
```

### Verify the running container

```bash
docker ps
```

### Test application health

```bash
curl http://localhost:5000/health
```

**Execution Result:** The Docker image was built successfully, the container was started, and the application health endpoint returned a successful response.

## 11. Docker Hub Image Registry

Docker Hub is used as the central container image registry.

**Docker Hub Repository:**

https://hub.docker.com/r/kinnaripatil/aceest-fitness

Published image:

`kinnaripatil/aceest-fitness:v1.0`

Docker commands:

```bash
docker tag aceest-fitness:v1.0 \
  kinnaripatil/aceest-fitness:v1.0

docker login

docker push kinnaripatil/aceest-fitness:v1.0
```

The versioned image provides a reusable deployment artifact.

## 12. SonarQube Static Code Analysis

SonarQube is integrated into the project to evaluate source code quality and identify potential code issues.

Configuration is maintained in:

`sonar-project.properties`

The analysis evaluates:

- Bugs
- Vulnerabilities
- Code smells
- Security hotspots
- Code quality

### Analysis Results

The completed SonarQube analysis reported:

| Metric | Result |
|---|---:|
| Bugs | 0 |
| Vulnerabilities | 0 |
| Code Smells | 0 |
| Security Hotspots | 1 |
| Code Coverage | 0% |
| Quality Gate | Passed |

The security hotspot should be reviewed separately. A passed Quality Gate does not mean that every security hotspot has been reviewed or resolved.

## 13. Kubernetes Deployment Configuration

Kubernetes YAML manifests are provided in the `kubernetes/` directory to demonstrate application deployment and different release strategies.

### Standard Deployment

`deployment.yaml`

- Uses a Kubernetes Deployment.
- Configures two application replicas.
- Defines container port 5000.
- Includes readiness and liveness probes using `/health`.

### Service Configuration

`service.yaml`

Defines the Kubernetes Service configuration for exposing the application internally.

### Deployment Strategies

The project includes configuration examples for the following strategies:

| Strategy | Configuration |
|---|---|
| Rolling Update | `rolling-update.yaml` |
| Blue-Green Deployment | `blue-green.yaml` |
| Canary Release | `canary.yaml` |
| Shadow Deployment | `shadow.yaml` |
| A/B Testing | `ab-testing.yaml` |

These manifests provide deployment configuration examples. A live Kubernetes cluster deployment and runtime validation of traffic shifting, traffic mirroring, and all five release strategies have not been completed.

For production-style traffic management, an Ingress controller or service mesh may be required.

## 14. Rollback Strategy

Kubernetes supports rolling back a Deployment to a previous revision when a deployment introduces problems.

Example commands:

```bash
kubectl rollout history deployment/aceest-fitness
```

```bash
kubectl rollout undo deployment/aceest-fitness
```

```bash
kubectl rollout status deployment/aceest-fitness
```

These commands describe the rollback procedure; successful execution against a live cluster remains to be verified.

## 15. Challenges and Solutions

| Challenge | Resolution |
|---|---|
| Jenkins Docker permission issue | Added the Jenkins user to the Docker group and restarted Jenkins. |
| SonarQube Java compatibility issue | Configured SonarQube to use the available Java 17 runtime. |
| Docker image creation | Built and tagged the Flask application image. |
| Application health validation | Verified the `/health` endpoint through the running container. |
| Kubernetes tooling limitations | Prepared Kubernetes YAML deployment and release strategy configurations; live cluster execution remains pending. |

## 16. Screenshots and Execution Evidence

The `Screenshots/` directory contains evidence of the assignment implementation, including:

- VM environment and tool versions.
- GitHub repository.
- Pytest execution.
- Docker image build and running container.
- Jenkins dashboard and successful pipeline.
- SonarQube project and analysis.
- Docker Hub image.
- Flask application execution.

## 17. Conclusion

This assignment demonstrates the implementation of core DevOps practices for the ACEest Fitness & Gym application.

The project integrates GitHub-based source control, automated testing using Pytest, Jenkins pipeline automation, Docker containerization, Docker Hub image publishing, and SonarQube code quality analysis.

Kubernetes deployment manifests have also been prepared to demonstrate multiple deployment strategies and rollback procedures.

The implementation provides a foundation for a repeatable CI/CD workflow and highlights the importance of automation, testing, containerization, code quality, and deployment management in modern software delivery.

---

**Project:** ACEest Fitness & Gym — DevOps Assignment 2  
**Student:** Patil Kinnari Nilesh Kamini  
**BITS ID:** 2025TM93044  
**Repository:** https://github.com/kinnari0403/ACEest-DevOps-Assignment-2
