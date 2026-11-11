# CI/CD Pipeline with Gitea + Jenkins

A production-style CI/CD pipeline built with Docker, automating the full 
build and deployment lifecycle.

## Tech Stack
- **Docker & Docker Compose** — containerized infrastructure
- **Gitea** — self-hosted Git server
- **Jenkins** — automated build and deploy pipeline
- **Node.js** — sample application
- **Docker Hub** — image registry

## How it works
1. Developer pushes code to Gitea
2. Gitea sends a webhook to Jenkins
3. Jenkins automatically:
   - Pulls the latest code
   - Installs dependencies
   - Runs tests
   - Builds a Docker image
   - Pushes the image to Docker Hub

## Pipeline Stages
Checkout → Install Dependencies → Run Tests → Build Image → Push to Docker Hub

## Setup & Run

### Prerequisites
- Docker Desktop
- Docker Compose

### Start the pipeline infrastructure
```bash
docker-compose up -d
```

### Access the services
| Service | URL |
|---|---|
| Gitea | http://localhost:3001 |
| Jenkins | http://localhost:8080 |

## Docker Hub Image
[thimal77/cicd-demo-app](https://hub.docker.com/r/thimal77/cicd-demo-app)