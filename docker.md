# Docker Command Reference

Docker is a containerization platform that allows developers to package applications and their dependencies into lightweight, portable containers. These containers can run consistently across development, testing, and production environments.

A container includes everything required to run an application such as libraries, runtime, and system tools. This makes applications portable across different systems.

Docker is widely used in modern **DevOps workflows**, CI/CD pipelines, and microservices architectures.

---

# Table of Contents

1. [Introduction to Docker](#introduction-to-docker)
2. [Prerequisites](#prerequisites)
3. [Docker Architecture](#docker-architecture)
4. [Docker Setup and Information](#docker-setup-and-information)
5. [Image Management](#image-management)
6. [Container Management](#container-management)
7. [Volume Management](#volume-management)
8. [Networking](#networking)
9. [Docker Compose](#docker-compose)
10. [Dockerfile Essentials](#dockerfile-essentials)
11. [Best Practices](#best-practices)
12. [Cleanup Commands](#cleanup-commands)
13. [Common Docker Workflow (Development)](#common-docker-workflow-development)
14. [Additional Resources](#additional-resources)

---

# Introduction to Docker

Docker solves the classic problem of **"It works on my machine"** by packaging applications along with all dependencies into containers.

A container ensures that the same environment runs everywhere, eliminating inconsistencies between development, testing, and production systems.

Key advantages of Docker include:

* Environment consistency
* Lightweight virtualization
* Faster application deployment
* Improved resource utilization
* Simplified DevOps workflows

**Example:**  
Suppose a developer builds a Node.js application that works correctly on their laptop but fails on the production server due to different library versions. By packaging the application inside a Docker container, the exact environment can be replicated on any machine.

**Example command:**
```bash
docker run nginx
```
This downloads the nginx image (if not already present) and starts a container running the nginx web server.

---

# Prerequisites

Before using Docker, ensure:

- Docker is installed ([official guide](https://docs.docker.com/get-docker/))
- Your user has permission to run Docker commands (on Linux, add user to `docker` group: `sudo usermod -aG docker $USER`)
- Docker daemon is running

Verify with:
```bash
docker --version
```

---

# Docker Architecture

Docker follows a **client-server architecture**.

The Docker client communicates with the Docker daemon, which performs the heavy work of building, running, and managing containers.

### Docker Client
The command-line interface used to interact with Docker.  
Example: `docker run nginx` – the client sends the request to the daemon.

### Docker Daemon (`dockerd`)
Runs in the background, managing images, containers, networks, and volumes.  
Example: `docker build -t myapp .` – the daemon reads the Dockerfile and builds the image.

### Docker Images
**Read-only templates** used to create containers. They contain the application code, runtime, libraries, and dependencies.  
Images are stored in registries like Docker Hub.  
Example images: `nginx`, `node`, `ubuntu`, `mysql`  
Command: `docker pull ubuntu`

### Docker Containers
**Running instances of Docker images**. They provide an isolated environment and share the host OS kernel (lightweight compared to VMs).  
Example: `docker run -it ubuntu` – starts an interactive Ubuntu container.

---

# Docker Setup and Information

| Command            | Description                                   |
| ------------------ | --------------------------------------------- |
| `docker --version` | Displays the installed Docker version         |
| `docker info`      | Shows detailed system-wide Docker information |
| `docker help`      | Lists all available Docker commands           |

**Example:**
```bash
docker --version
```
Output: `Docker version 26.1.4, build 5650f9b`

---

# Image Management

| Command                                      | Description                                     |
| -------------------------------------------- | ----------------------------------------------- |
| `docker images`                              | Lists all locally available Docker images       |
| `docker pull <image>`                        | Downloads an image from Docker Hub              |
| `docker rmi <image>`                         | Removes a Docker image                          |
| `docker image inspect <image>`               | Displays detailed image information             |
| `docker image prune`                         | Removes unused images                           |
| `docker build -t <image_name>:<tag> .`       | Builds an image from a Dockerfile (tag optional)|
| `docker tag <source_image> <target:tag>`     | Assigns a new tag to an existing image          |
| `docker save -o archive.tar <image>`         | Saves an image to a tar file                    |
| `docker load -i archive.tar`                 | Loads an image from a tar file                  |

**Example:**
```bash
docker build -t my-node-app:1.0 .
```
Builds an image named `my-node-app` with tag `1.0` using the Dockerfile in the current directory.

---

# Container Management

| Command                                      | Description                                     |
| -------------------------------------------- | ----------------------------------------------- |
| `docker ps`                                  | Lists running containers                        |
| `docker ps -a`                               | Lists all containers (including stopped)        |
| `docker run <image>`                         | Creates and starts a container                  |
| `docker run -it <image>`                     | Runs container interactively (e.g., `bash`)     |
| `docker run -d <image>`                      | Runs container in background (detached)         |
| `docker run --name <name> <image>`           | Runs container with a custom name               |
| `docker run -p <host_port>:<container_port>` | Maps a host port to a container port            |
| `docker exec -it <container> /bin/bash`      | Accesses a running container’s shell           |
| `docker start <container>`                   | Starts a stopped container                      |
| `docker stop <container>`                    | Stops a running container                       |
| `docker restart <container>`                 | Restarts a container                            |
| `docker rm <container>`                      | Removes a container (use `-f` to force)         |
| `docker logs <container>`                    | Views container logs (add `-f` to follow)       |
| `docker logs -f <container>`                 | Follows log output in real time                 |
| `docker inspect <container>`                 | Displays detailed container metadata            |
| `docker stats`                               | Shows real-time resource usage of all containers|
| `docker cp <container>:<src_path> <dest>`    | Copies files/folders from container to host     |
| `docker cp <src> <container>:<dest_path>`    | Copies files/folders from host to container     |
| `docker commit <container> <new_image>`      | Creates a new image from a container (not recommended for production) |
| `docker attach <container>`                  | Attaches to a running container’s main process  |

**Example:**
```bash
docker run -d -p 80:80 --name webserver nginx
```
Runs an nginx container in detached mode, maps host port 80 to container port 80, and names it `webserver`.

---

# Volume Management

Volumes persist data even after containers are removed. Without volumes, container data is lost when the container stops.

| Command                                                        | Description                             |
| -------------------------------------------------------------- | --------------------------------------- |
| `docker volume create <volume_name>`                           | Creates a new volume                    |
| `docker volume ls`                                             | Lists all volumes                       |
| `docker volume inspect <volume_name>`                          | Shows volume details                    |
| `docker volume rm <volume_name>`                               | Removes a volume                        |
| `docker run -v <volume_name>:<container_path> <image>`         | Mounts a volume (old syntax)            |
| `docker run --mount source=<volume_name>,target=<container_path> <image>` | Mounts a volume (explicit syntax, recommended) |

**Example:**
```bash
docker run -v myvolume:/data ubuntu
```
Mounts the volume `myvolume` inside the container at `/data`.

**Tip:** Use `--mount` for better readability:
```bash
docker run --mount source=myvolume,target=/data ubuntu
```

---

# Networking

Docker networking allows containers to communicate with each other and with external systems.

| Command                                             | Description                                   |
| --------------------------------------------------- | --------------------------------------------- |
| `docker network ls`                                 | Lists all networks                            |
| `docker network create <network_name>`              | Creates a custom bridge network               |
| `docker network inspect <network_name>`             | Shows detailed network configuration          |
| `docker network rm <network_name>`                  | Removes a network                             |
| `docker run --network <network_name> <image>`       | Attaches a container to a specific network    |
| `docker network connect <network_name> <container>` | Connects an existing container to a network   |
| `docker network disconnect <network_name> <container>` | Disconnects a container from a network    |

### Common Network Drivers
| Driver   | Description                                                                 |
| -------- | --------------------------------------------------------------------------- |
| `bridge` | Default, private network on the host. Containers can communicate via IP.    |
| `host`   | Container shares the host’s network stack (no isolation, high performance). |
| `overlay`| Connects containers across multiple Docker daemons (Swarm / Kubernetes).    |
| `none`   | No network access.                                                          |

**Example:**
```bash
docker network create mynetwork
docker run --network mynetwork --name app1 nginx
docker run --network mynetwork --name app2 nginx
```
Both containers can now reach each other using their container names as hostnames.

---

# Docker Compose

Docker Compose defines and runs **multi-container applications** using a YAML file.  
**Note:** Modern Docker uses `docker compose` (no hyphen). The legacy `docker-compose` (with hyphen) still works but is deprecated.

### Example `docker-compose.yml` (web app + redis)

```yaml
version: '3.8'

services:
  web:
    image: nginx
    ports:
      - "80:80"
    depends_on:
      - redis

  redis:
    image: redis:alpine
    volumes:
      - redis_data:/data

volumes:
  redis_data:
```

### Useful Commands

| Command                         | Description                                     |
| ------------------------------- | ----------------------------------------------- |
| `docker compose up`             | Starts all services (attached to terminal)      |
| `docker compose up -d`          | Starts services in the background (detached)    |
| `docker compose down`           | Stops and removes containers, networks          |
| `docker compose down -v`        | Also removes named volumes declared in the file |
| `docker compose ps`             | Lists running services                          |
| `docker compose logs`           | Shows logs from all services                    |
| `docker compose logs -f <service>` | Follows logs of a specific service           |
| `docker compose build`          | Rebuilds services (if a Dockerfile is used)     |
| `docker compose exec <service> <command>` | Runs a command inside a service container |

**Example:**
```bash
docker compose up -d
docker compose logs -f web
docker compose down
```

---

# Dockerfile Essentials

A Dockerfile is a script of instructions to build a Docker image.

### Example Dockerfile (Node.js app)

```dockerfile
# Base image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package files first (better layer caching)
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy the rest of the application
COPY . .

# Create a non-root user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001
USER nodejs

# Expose port
EXPOSE 3000

# Start command
CMD ["node", "server.js"]
```

### Multi‑stage Build Example (Go app)

```dockerfile
# Stage 1: Build
FROM golang:1.21 AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o myapp .

# Stage 2: Runtime
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/myapp .
CMD ["./myapp"]
```

### Important Dockerfile Instructions

| Instruction   | Description                                          |
| ------------- | ---------------------------------------------------- |
| `FROM`        | Defines the base image (use `-alpine` for smaller size) |
| `WORKDIR`     | Sets the working directory for subsequent commands  |
| `COPY`        | Copies files from host to container                 |
| `ADD`         | Like `COPY` but supports URLs and auto‑extract tar  |
| `RUN`         | Executes commands during the image build            |
| `ENV`         | Sets environment variables                           |
| `EXPOSE`      | Documents which port the container listens on       |
| `USER`        | Switches to a non‑root user for security            |
| `CMD`         | Default command when container starts (can be overridden) |
| `ENTRYPOINT`  | Similar to `CMD` but harder to override (use for fixed executables) |

---

# Best Practices

For production environments:

1. **Use official or verified base images** (e.g., `node:18-alpine`)
2. **Keep images small** – use alpine variants, multi‑stage builds, and clean up temporary files
3. **Leverage build cache** – order `COPY` commands from least to most frequently changed
4. **Run as non‑root user** – create a user inside the container
5. **Use `.dockerignore`** – exclude `node_modules`, `.git`, `.env`, logs
6. **Tag images with versions** – avoid `latest` in production
7. **Use environment variables for configuration** – never hardcode secrets
8. **Scan images for vulnerabilities** – `docker scan <image>` or use third‑party tools
9. **Set resource limits** – `docker run --memory="512m" --cpus="1.0"`

### Example `.dockerignore`
```
node_modules
.git
.env
*.log
Dockerfile
README.md
```

---

# Cleanup Commands

| Command                       | Description                                         |
| ----------------------------- | --------------------------------------------------- |
| `docker system prune`         | Removes stopped containers, unused networks, dangling images, and build cache |
| `docker system prune -a`      | Also removes all unused images (not just dangling)  |
| `docker container prune`      | Removes only stopped containers                     |
| `docker image prune`          | Removes unused images (dangling)                    |
| `docker image prune -a`       | Removes all images not used by any container        |
| `docker volume prune`         | Removes unused volumes (⚠️ data loss)               |
| `docker network prune`        | Removes unused networks                             |

**Example:**
```bash
docker system prune -a --volumes
```
⚠️ **Caution:** This removes all stopped containers, unused networks, dangling images, and unused volumes. Use with care.

---

# Common Docker Workflow (Development)

Typical day‑to‑day workflow for a developer:

1. **Write a Dockerfile** (and `.dockerignore`)
2. **Build the image**
   ```bash
   docker build -t myapp:latest .
   ```
3. **Run the container** (with port mapping and volume for live code)
   ```bash
   docker run -p 3000:3000 -v $(pwd):/app myapp:latest
   ```
4. **Verify it's running**
   ```bash
   docker ps
   ```
5. **View logs**
   ```bash
   docker logs -f <container_id>
   ```
6. **Stop and remove when done**
   ```bash
   docker stop <container_id>
   docker rm <container_id>
   ```
7. **Push to a registry** (optional)
   ```bash
   docker tag myapp:latest myusername/myapp:1.0
   docker push myusername/myapp:1.0
   ```

---

# Additional Resources

- [Docker Official Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Awesome Docker (curated list)](https://github.com/veggiemonk/awesome-docker)

---

# Support

If this reference helps you, consider giving it a ⭐ on GitHub. Your support encourages more improvements!
