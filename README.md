# CV Platform

Mini DevOps project showcasing a containerized CV website with automated CI/CD using Docker and Jenkins.

## Overview

This project started as a simple Bash-based CV deployment idea and evolved into a small DevOps lab environment combining:

- Docker
- Docker Compose
- Jenkins
- NGINX
- GitHub
- Docker Hub
- Linux troubleshooting

The goal was to better understand how CI/CD pipelines, containers and Linux concepts work together in a real workflow.

---

# Architecture

## Application Container

The CV website is served using an NGINX container.

The application image is built from `app/Dockerfile`.

Static HTML files are copied into the default NGINX web root.

---

## Jenkins Container

A custom Jenkins image is used to provide:

- Jenkins
- Docker CLI
- CI/CD pipeline support

The Jenkins image is built from `jenkins/Dockerfile`.

Docker socket mounting is used so Jenkins can communicate with the Docker daemon running on the host.

---

# Project Structure

```text
cv-platform/
├── app/
│   ├── Dockerfile
│   └── site/
│
├── jenkins/
│   └── Dockerfile
│
├── docker-compose.yml
├── Jenkinsfile
└── README.md
```

---

# CI/CD Pipeline

The Jenkins pipeline performs the following stages:

| Stage | Description |
|---|---|
| Build | Builds Docker image for CV website |
| Test | Runs temporary container and validates site using curl |
| Push | Uploads image to Docker Hub |
| Deploy | Replaces running production container |

---

# Running the Environment

Start the full environment using Docker Compose:

```bash
docker compose up -d --build
```

Jenkins will be available on:

`http://HOST_IP:8091`

The CV website will be available on:

`http://HOST_IP:8090`

---

# Lessons Learned

This project involved troubleshooting several real-world DevOps issues including:

- Docker socket permissions
- Linux group ID (GID) mismatches between host and containers
- Container networking and localhost isolation
- Docker build contexts
- Jenkins pipeline troubleshooting
- Persistent Docker volumes
- Docker Hub authentication inside Jenkins containers

---

# Future Improvements

- GitHub webhook automation
- Kubernetes deployment
- Jenkins Configuration as Code (JCasC)
- Automated rollback strategy
- Reverse proxy integration
