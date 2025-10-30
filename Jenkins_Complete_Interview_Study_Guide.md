
# Jenkins Complete Interview & Practical Study Guide

This guide covers **everything you need to know about Jenkins** for interviews and hands-on DevOps work — from installation to pipelines, integration with Git, Docker, and AWS, plus troubleshooting and best practices.

---

## 🧠 1. What is Jenkins?

**Answer:**
Jenkins is an **open-source automation server** that helps automate parts of the software development process like **building, testing, and deploying applications**. It’s the core tool for implementing **Continuous Integration (CI)** and **Continuous Delivery (CD)**.

**Key Features:**
- Open-source and community-driven  
- 1000+ plugins for integration (Git, Docker, Kubernetes, AWS, etc.)  
- Supports pipelines as code (Declarative & Scripted)  
- Easy web-based UI  
- Distributed builds using master-agent architecture  

---

## ⚙️ 2. Jenkins Architecture

**Components:**
- **Jenkins Master** – Controls the build process and assigns jobs to agents.
- **Jenkins Agent (Slave)** – Executes tasks/jobs assigned by the master.
- **Build Queue** – Holds jobs waiting to execute.
- **Executor** – A slot that runs a job on a node.

**Flow:**
1. Developer commits code to GitHub.  
2. Jenkins detects change via Webhook.  
3. Jenkins fetches the code, builds it, and runs tests.  
4. Jenkins deploys to a test/staging/production server.  

---

## 🧩 3. Installing Jenkins

**On Ubuntu:**
```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
```
Access Jenkins at: **http://<your_ip>:8080**

**Default unlock path:** `/var/lib/jenkins/secrets/initialAdminPassword`

---

## 🧾 4. Jenkins Pipeline Basics

### What is a Pipeline?
A pipeline is a series of steps that define the CI/CD process in Jenkins.

### Two Types:
1. **Declarative Pipeline (simpler, structured)**  
2. **Scripted Pipeline (Groovy-based, flexible)**

**Example Declarative Pipeline:**
```groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/user/repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
```

---

## 🔗 5. Integration with Git

**To connect Jenkins to GitHub:**
1. Install **Git Plugin** in Jenkins.
2. Configure global Git in **Manage Jenkins → Global Tool Configuration**.
3. Create a Jenkins job → SCM → Git → Enter repo URL.
4. Optionally add **GitHub webhook** for automation.

**Webhook Setup (GitHub → Jenkins):**
- Go to GitHub repo → Settings → Webhooks → Add webhook  
- Payload URL: `http://<jenkins-server-ip>:8080/github-webhook/`  
- Content type: `application/json`  
- Events: “Just the push event”  

---

## 🧪 6. Jenkins with Docker

### Run Jenkins in Docker
```bash
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins     -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```

### Use Jenkins to Build Docker Images
In a pipeline:
```groovy
pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("myapp:${env.BUILD_ID}")
                }
            }
        }
    }
}
```

---

## ☁️ 7. Jenkins with AWS

**Integration Options:**
- Install **AWS Credentials Plugin**
- Use AWS CLI inside pipeline
- Configure IAM user and credentials

**Example: Deploying to S3**
```groovy
pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws_access_key')
        AWS_SECRET_ACCESS_KEY = credentials('aws_secret_key')
    }
    stages {
        stage('Deploy to S3') {
            steps {
                sh 'aws s3 cp app.zip s3://mybucket/app.zip'
            }
        }
    }
}
```

---

## 🧰 8. Common Jenkins Interview Questions

**Q1: What is the difference between Freestyle and Pipeline jobs?**  
**A:** Freestyle is basic with GUI-based steps. Pipeline jobs define the process as code, allowing version control and automation.

**Q2: What are Jenkins Agents?**  
**A:** Machines that run build tasks assigned by the Jenkins master.

**Q3: How can you trigger builds automatically?**  
**A:** Using Webhooks, cron jobs, or post-commit hooks.

**Q4: How do you secure Jenkins?**  
**A:**  
- Enable authentication (Matrix or Role-based security)  
- Limit admin access  
- Use HTTPS  
- Update plugins regularly  

**Q5: How can Jenkins be integrated with Terraform or Ansible?**  
**A:** By adding shell or pipeline steps to run `terraform plan/apply` or `ansible-playbook` commands.

**Q6: What is a Jenkinsfile?**  
**A:** A text file containing the pipeline as code, stored in the project’s root directory.

**Q7: What happens if Jenkins crashes during a build?**  
**A:** The build is interrupted; Jenkins can be configured with checkpoints or resumable pipelines.

**Q8: How do you handle credentials securely in Jenkins?**  
**A:** Using Jenkins **Credentials Manager** and referencing them via `credentials()` function in pipelines.

---

## 🔍 9. Troubleshooting Jenkins

**Common Issues:**
| Problem | Solution |
|----------|-----------|
| Jenkins not starting | Check `systemctl status jenkins` or `/var/log/jenkins/jenkins.log` |
| Build fails unexpectedly | Check console output & workspace permissions |
| Webhook not triggering | Validate payload URL and GitHub webhook logs |
| Plugin errors | Reinstall plugin or check compatibility with Jenkins version |

---

## 🏁 10. Best Practices

- Keep Jenkins and plugins up to date  
- Use **Pipeline as Code** (Jenkinsfile)  
- Backup Jenkins Home (`/var/lib/jenkins`) regularly  
- Use **shared libraries** for reusable pipeline code  
- Use **Docker agents** for consistency  
- Monitor Jenkins with Prometheus/Grafana  

---

## 🧩 11. Example CI/CD Pipeline (Git → Jenkins → Docker → AWS)

```groovy
pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws_access_key')
        AWS_SECRET_ACCESS_KEY = credentials('aws_secret_key')
    }
    stages {
        stage('Clone') {
            steps { git 'https://github.com/user/app.git' }
        }
        stage('Build') {
            steps { sh 'docker build -t app .' }
        }
        stage('Test') {
            steps { sh 'docker run app pytest tests/' }
        }
        stage('Push') {
            steps { sh 'docker push myrepo/app:latest' }
        }
        stage('Deploy') {
            steps { sh 'aws ecs update-service --cluster mycluster --service myapp --force-new-deployment' }
        }
    }
}
```

---

## 🧾 12. Quick Revision Sheet

| Concept | Command / Tip |
|----------|----------------|
| Restart Jenkins | `sudo systemctl restart jenkins` |
| Unlock Jenkins | `/var/lib/jenkins/secrets/initialAdminPassword` |
| Backup Jenkins | Copy `/var/lib/jenkins` directory |
| View logs | `/var/log/jenkins/jenkins.log` |
| List plugins | `Manage Jenkins → Plugin Manager` |
| Run job via CLI | `java -jar jenkins-cli.jar build <job_name>` |

---

## ✅ Final Tip

> Practice by creating a **multi-branch pipeline** that automatically builds and deploys your app whenever you push to GitHub. Once you do that confidently, you can handle **any Jenkins interview question** with ease.

---
