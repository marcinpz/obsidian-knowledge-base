# Docker Basics

## What is Docker?
- **Definition**: A platform for containerization, packaging apps with their dependencies
- **Purpose**: Consistent environments across dev, test, and prod
- **Core Idea**: "Build once, run anywhere"

## Key Concepts
- **Container**: Lightweight, isolated runtime environment
- **Image**: Read-only template to create containers
- **Dockerfile**: Script to build images
- **Registry**: Storage for images (e.g., Docker Hub)

## Basic Commands
- **Run a Container**:
  ```bash
  docker run -it ubuntu bash
  ```
  - `-it`: Interactive terminal
- **List Containers**:
  ```bash
  docker ps -a
  ```
  - `-a`: Show all (running + stopped)
- **Build Image**:
  ```bash
  docker build -t myapp:1.0 .
  ```
  - `-t`: Tag name
- **Push to Registry**:
  ```bash
  docker push myapp:1.0
  ```

## Dockerfile Example
```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```
- Builds a Node.js app image

## Components
- **Docker Engine**: Runs containers (client-server architecture)
- **Docker CLI**: Command-line interface
- **Docker Compose**: Manages multi-container apps
  ```yaml
  version: '3'
  services:
    web:
      image: myapp:1.0
      ports:
        - "3000:3000"
  ```

## Networking
- **Bridge**: Default, containers talk via internal network
  ```bash
  docker network ls
  ```
- **Host**: Container uses host’s network
- **Ports**: Map container ports to host
  ```bash
  docker run -p 8080:80 nginx
  ```

## Volumes
- **Purpose**: Persist data outside containers
- **Mount**:
  ```bash
  docker run -v /host/path:/container/path myimage
  ```
- **Named Volume**:
  ```bash
  docker volume create mydata
  docker run -v mydata:/app/data myimage
  ```

## Use Cases
- **DevOps**: CI/CD pipelines, microservices
- **Testing**: Isolated environments
- **Deployment**: Consistent prod setups

## Common Commands
- **Stop Container**:
  ```bash
  docker stop <container_id>
  ```
- **Remove Container**:
  ```bash
  docker rm <container_id>
  ```
- **Remove Image**:
  ```bash
  docker rmi <image_id>
  ```
- **Logs**:
  ```bash
  docker logs <container_id>
  ```

## Tips for DevOps
- **Optimize Images**: Use multi-stage builds
  ```dockerfile
  FROM golang:1.18 AS builder
  RUN go build -o app
  FROM alpine
  COPY --from=builder /app .
  ```
- **Security**: Avoid running as root, scan images
- **Orchestration**: Pair with Kubernetes or Swarm

## Challenges
- **Storage**: Managing persistent data
- **Networking**: Complex in multi-container setups
- **Resource Use**: Monitor CPU/memory

> **Tip**: Start with `docker run hello-world` to verify setup!