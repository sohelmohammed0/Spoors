
# 🐳 Docker Complete Interview & Practical Study Guide

This guide will help you **master Docker for DevOps and interviews**. It covers all key concepts, real-world use cases, and interview questions with detailed answers — ensuring you can confidently answer at least 90% of Docker questions.

---

## 🚀 1. What is Docker?

**Answer:**
Docker is an **open-source platform** that allows you to **build, package, and run applications** in **containers** — lightweight, portable, and isolated environments that ensure consistency across development and production.

**Key Benefits:**
- Lightweight (uses OS-level virtualization)
- Consistent across environments
- Fast deployment and scalability
- Simplifies CI/CD pipelines

---

## 🧩 2. Key Docker Components

| Component | Description |
|------------|--------------|
| **Image** | A blueprint for containers (read-only template). |
| **Container** | A running instance of an image. |
| **Dockerfile** | A script with instructions to build an image. |
| **Docker Engine** | Core part that builds and runs containers. |
| **Docker Hub** | Public registry to share and download Docker images. |
| **Docker Compose** | Tool to manage multi-container applications. |

---

## 🧱 3. Docker Architecture

- **Docker Client** – CLI used to interact with Docker daemon.  
- **Docker Daemon (dockerd)** – Manages containers, images, and networks.  
- **Docker Registry** – Stores Docker images (e.g., Docker Hub).  
- **Docker Objects** – Images, Containers, Networks, Volumes.

**Flow:**
1. You run `docker run` command.  
2. Docker client talks to daemon.  
3. Daemon checks image → pulls if needed → creates and runs container.

---

## 🧰 4. Common Docker Commands

| Task | Command |
|------|----------|
| Check Docker version | `docker --version` |
| Pull image | `docker pull nginx` |
| List images | `docker images` |
| Run container | `docker run -d -p 8080:80 nginx` |
| List running containers | `docker ps` |
| Stop container | `docker stop <container_id>` |
| Remove container | `docker rm <container_id>` |
| Remove image | `docker rmi <image_id>` |
| View logs | `docker logs <container_id>` |
| Access container shell | `docker exec -it <container_id> /bin/bash` |

---

## 🧾 5. Dockerfile Explained

**Dockerfile Example:**
```Dockerfile
# Use a base image
FROM python:3.10

# Set working directory
WORKDIR /app

# Copy app files
COPY . .

# Install dependencies
RUN pip install -r requirements.txt

# Expose port
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]
```

**Command Breakdown:**
| Instruction | Description |
|--------------|-------------|
| `FROM` | Base image to start from |
| `WORKDIR` | Set working directory |
| `COPY` | Copy files from local to container |
| `RUN` | Execute command during build |
| `EXPOSE` | Specify port the app listens on |
| `CMD` | Command to execute when container runs |

---

## 🧠 6. Docker Image Lifecycle

1. **Build** – `docker build -t myapp .`  
2. **Run** – `docker run -d myapp`  
3. **Push** – `docker push myrepo/myapp`  
4. **Pull** – `docker pull myrepo/myapp`  

---

## 🧩 7. Docker Networking

| Network Type | Description |
|---------------|-------------|
| **Bridge** | Default network for standalone containers |
| **Host** | Shares the host’s network namespace |
| **None** | Container has no networking |
| **Overlay** | Used for multi-host communication (Swarm) |
| **Macvlan** | Assigns MAC address to container for direct access |

**Commands:**
```bash
docker network ls
docker network inspect bridge
docker network create mynet
docker run -d --network=mynet nginx
```

---

## 📦 8. Docker Volumes (Data Persistence)

Volumes let data persist even after containers are deleted.

```bash
docker volume create mydata
docker run -d -v mydata:/data nginx
```

**Types of storage:**
- **Volumes** (preferred)
- **Bind mounts**
- **tmpfs** (temporary storage in memory)

---

## ⚙️ 9. Docker Compose

Used for defining and managing **multi-container** applications.

**docker-compose.yml Example:**
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
```

**Commands:**
```bash
docker-compose up -d
docker-compose ps
docker-compose down
```

---

## 🧪 10. Docker in CI/CD (with Jenkins)

**Pipeline Example:**
```groovy
pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'docker run myapp:latest pytest'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push myapp:latest'
                }
            }
        }
    }
}
```

---

## ☁️ 11. Docker with AWS

- Use **Amazon ECR** (Elastic Container Registry) for image storage.  
- Deploy containers on **ECS**, **EKS**, or **Fargate**.  

**Commands:**
```bash
aws ecr create-repository --repository-name myapp
$(aws ecr get-login --no-include-email)
docker tag myapp:latest <aws_account_id>.dkr.ecr.region.amazonaws.com/myapp
docker push <aws_account_id>.dkr.ecr.region.amazonaws.com/myapp
```

---

## 🧩 12. Common Interview Questions (With Answers)

**Q1: What is the difference between a VM and a Container?**  
**A:** VM virtualizes hardware, while containers virtualize OS. Containers are lightweight and start instantly.

**Q2: What is the difference between `COPY` and `ADD` in Dockerfile?**  
**A:** `COPY` copies local files; `ADD` can also extract `.tar` files and fetch URLs.

**Q3: What is a Docker namespace?**  
**A:** It isolates resources like process IDs, networks, and mounts between containers.

**Q4: How can you reduce Docker image size?**  
**A:** Use smaller base images (e.g., `alpine`), combine RUN commands, clean cache.

**Q5: How to view logs of a container?**  
**A:** `docker logs <container_id>`

**Q6: What is a multi-stage build?**  
**A:** Allows building and packaging in one Dockerfile while keeping the final image minimal.

**Q7: How do you handle secrets in Docker?**  
**A:** Use environment variables, Docker Secrets (in Swarm), or external secret managers.

**Q8: How do containers communicate?**  
**A:** Through Docker networks; by default, all containers on the same bridge network can talk via IP or container name.

**Q9: How to remove all stopped containers and unused images?**  
**A:** `docker system prune -a`

**Q10: What are health checks in Docker?**  
**A:** Used to check if a container is healthy or not using `HEALTHCHECK` instruction.

---

## 🔍 13. Troubleshooting Docker

| Issue | Command / Fix |
|--------|----------------|
| Container not starting | `docker logs <container_id>` |
| Image build fails | Check Dockerfile syntax or dependencies |
| Container exits immediately | Ensure CMD keeps container running |
| “Port already in use” | Use another port with `-p <new_port>:<container_port>` |
| Docker daemon not running | `sudo systemctl start docker` |

---

## 🧾 14. Best Practices

- Use **.dockerignore** to exclude unnecessary files  
- Tag images meaningfully (`app:v1.0`)  
- Keep Dockerfiles simple and modular  
- Use health checks and restart policies  
- Regularly clean up unused images and volumes  
- Scan images for vulnerabilities (`docker scan`)  

---

## 🏁 15. Quick Revision Commands

| Purpose | Command |
|----------|----------|
| Build image | `docker build -t myapp .` |
| Run container | `docker run -d -p 8080:80 myapp` |
| List all containers | `docker ps -a` |
| Stop container | `docker stop <id>` |
| Remove container | `docker rm <id>` |
| Remove image | `docker rmi <id>` |
| Show logs | `docker logs <id>` |
| Execute inside container | `docker exec -it <id> bash` |
| Clean unused resources | `docker system prune -a` |

---

## ✅ Final Tip

> Practice by containerizing a simple Python or Node.js app, push it to Docker Hub, and deploy it using Jenkins or AWS ECS. Once you do that, you’ll be ready for any Docker interview.

---
