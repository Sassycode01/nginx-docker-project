# 🚀 Nginx Docker CI/CD Project

## 📌 Project Overview

This project demonstrates a complete **CI/CD pipeline for deploying a containerized Nginx web application** using GitHub, Jenkins, Docker, Docker Hub, Docker Compose, and AWS EC2.

The application is packaged into a Docker container using Nginx and automatically built and deployed through a Jenkins CI/CD pipeline.

---

## 🏗️ Project Architecture

```text
Developer
    │
    ▼
  GitHub
    │
    │ Code Push
    ▼
  Jenkins
    │
    ├── Clone Repository
    ├── Build Docker Image
    ├── Test/Verify Image
    ├── Push Image
    │
    ▼
 Docker Hub
    │
    │ Pull Image
    ▼
 AWS EC2 (Ubuntu)
    │
    ▼
 Docker Container
    │
    ▼
   Nginx
    │
    ▼
 Web Browser
```

---

## 🛠️ Technologies Used

| Technology     | Purpose                  |
| -------------- | ------------------------ |
| AWS EC2        | Cloud server             |
| Ubuntu         | Server operating system  |
| Git            | Version control          |
| GitHub         | Source code repository   |
| Jenkins        | CI/CD automation         |
| Docker         | Containerization         |
| Docker Hub     | Docker image registry    |
| Docker Compose | Container management     |
| Nginx          | Web server               |
| SSH            | Secure server connection |
| HTML           | Web page                 |

---

## 📁 Project Structure

```text
mynginx-docker-project/
│
├── index.html
├── Dockerfile
├── docker-compose.yml
├── Jenkinsfile
└── README.md
```

---

# 1️⃣ Application

The project contains a simple HTML web page served through **Nginx**.

### `index.html`

The HTML file contains the website content that is displayed when users access the application.

---

# 2️⃣ Dockerfile

The Dockerfile creates an Nginx-based Docker image.

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

### Explanation

* `FROM nginx:latest` → Uses the official Nginx image.
* `COPY` → Copies our HTML page into the Nginx web directory.
* `EXPOSE 80` → Documents that the application uses port 80.

---

# 3️⃣ Build Docker Image

To build the Docker image manually:

```bash
docker build -t mynginx .
```

Check the image:

```bash
docker images
```

---

# 4️⃣ Run Docker Container

Run the Nginx container:

```bash
docker run -d -p 80:80 --name mynginx-container mynginx
```

Check running containers:

```bash
docker ps
```

The application can then be accessed through:

```text
http://<EC2-PUBLIC-IP>
```

---

# 5️⃣ Docker Compose

Docker Compose is used to simplify container deployment.

### `docker-compose.yml`

```yaml
version: '3.8'

services:
  nginx:
    image: <DOCKERHUB_USERNAME>/mynginx:latest
    container_name: mynginx-container
    ports:
      - "80:80"
    restart: unless-stopped
```

Replace:

```text
<DOCKERHUB_USERNAME>
```

with your Docker Hub username.

For example:

```yaml
image: Sassy2031/mynginx:latest
```

Start the application:

```bash
docker compose up -d
```

Check the container:

```bash
docker compose ps
```

Stop the application:

```bash
docker compose down
```

---

# 6️⃣ Docker Hub

The Docker image is pushed to Docker Hub so that it can be pulled and deployed on the AWS EC2 server.

### Login

```bash
docker login
```

### Tag Image

```bash
docker tag mynginx:latest <DOCKERHUB_USERNAME>/mynginx:latest
```

### Push Image

```bash
docker push <DOCKERHUB_USERNAME>/mynginx:latest
```

The image can then be pulled using:

```bash
docker pull <DOCKERHUB_USERNAME>/mynginx:latest
```

---

# 7️⃣ AWS EC2 Deployment

An **Ubuntu EC2 instance** was used as the deployment server.

### Connect to EC2

```bash
ssh -i <key-file>.pem ubuntu@<EC2-PUBLIC-IP>
```

After connecting, Docker is used to run the application.

---

## 🔐 AWS Security Group

The EC2 Security Group allows the required traffic.

Required ports:

| Port | Protocol | Purpose      |
| ---- | -------- | ------------ |
| 22   | TCP      | SSH          |
| 80   | TCP      | HTTP / Nginx |

Port 22 should preferably be restricted to your trusted IP rather than opened to everyone.

---

# 8️⃣ Jenkins CI/CD

Jenkins is used to automate the complete build and deployment process.

### Pipeline Flow

```text
GitHub Push
     ↓
Jenkins Trigger
     ↓
Checkout Code
     ↓
Build Docker Image
     ↓
Docker Login
     ↓
Push Image to Docker Hub
     ↓
Deploy/Update Container
     ↓
Application Running
```

---

# 9️⃣ Jenkins Pipeline

The Jenkins pipeline automates the Docker build and deployment process.

Example pipeline stages:

```text
Checkout
   ↓
Build Docker Image
   ↓
Docker Login
   ↓
Push Docker Image
   ↓
Deploy
```

The pipeline was successfully executed in Jenkins.

✅ **Build Successful**

---

# 🔄 CI/CD Workflow

Whenever code is updated:

### Step 1 — Developer changes the application

```text
index.html
```

### Step 2 — Commit changes

```bash
git add .
git commit -m "Update application"
```

### Step 3 — Push to GitHub

```bash
git push origin main
```

### Step 4 — Jenkins detects the change

Jenkins starts the pipeline.

### Step 5 — Docker image is rebuilt

```bash
docker build
```

### Step 6 — Image is pushed to Docker Hub

```bash
docker push
```

### Step 7 — EC2 deployment is updated

The latest Docker image is deployed.

### Step 8 — Nginx serves the updated application

The updated website becomes available through the EC2 public IP.

---

# 🔒 Security Practices

The project uses several basic security practices:

* Docker Hub credentials should be stored in **Jenkins Credentials** rather than hard-coded.
* SSH private keys should never be committed to GitHub.
* `.env` files containing secrets should not be pushed to GitHub.
* AWS Security Groups should restrict unnecessary ports.
* Docker Hub credentials should not be written directly inside source code.

---

# 🧪 Verification Commands

Check Docker containers:

```bash
docker ps
```

Check Docker images:

```bash
docker images
```

Check Docker Compose:

```bash
docker compose ps
```

View container logs:

```bash
docker logs mynginx-container
```

Test Nginx locally on the server:

```bash
curl http://localhost
```

---

# 🎯 Project Objectives

The main objectives of this project were:

* Learn Docker containerization
* Deploy an Nginx web application
* Understand Docker images and containers
* Use Docker Compose
* Push images to Docker Hub
* Deploy an application on AWS EC2
* Understand Git and GitHub workflow
* Build a Jenkins CI/CD pipeline
* Automate Docker image creation and deployment

---

# ✅ Project Status

```text
GitHub Repository       ✅
Dockerfile              ✅
Nginx Application       ✅
Docker Image            ✅
Docker Container        ✅
Docker Hub              ✅
Docker Compose          ✅
AWS EC2                 ✅
Jenkins CI/CD           ✅
Pipeline Execution      ✅
Application Deployment  ✅
```

## 🎉 Result

The project successfully demonstrates a basic **end-to-end DevOps CI/CD workflow**:

```text
GitHub
   ↓
Jenkins
   ↓
Docker Build
   ↓
Docker Hub
   ↓
AWS EC2
   ↓
Docker
   ↓
Nginx
   ↓
Web Application
```

---

# 👨‍💻 Skills Demonstrated

* Linux
* AWS EC2
* Git
* GitHub
* Jenkins
* Docker
* Docker Compose
* Docker Hub
* Nginx
* CI/CD
* SSH
* Basic cloud deployment
* Containerization

---

## 📌 Future Improvements

The project can be extended by adding:

* GitHub webhook → Jenkins automatic trigger
* Jenkins agents
* Docker image versioning
* Automated testing
* Terraform for AWS infrastructure
* SonarQube code-quality analysis
* Prometheus and Grafana monitoring
* Kubernetes deployment
* HTTPS using SSL/TLS
* Blue-green or rolling deployment

---

## ⭐ Conclusion

This project provides hands-on experience with the fundamental DevOps workflow of **source-code management, containerization, image management, CI/CD automation, and cloud deployment**.

It demonstrates how a simple web application can be automatically built, packaged, and deployed using modern DevOps tools.

