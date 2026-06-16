# Flask App with MySQL (Docker + Jenkins CI/CD)

This is a simple **Flask + MySQL two-tier application** that was already developed and containerized using Docker Compose.

I implemented **CI/CD automation using Jenkins** to automate the build, security scan, image push, and deployment process.

---

## 🚀 My Contribution

I worked on the following DevOps tasks:

- Configured Jenkins CI/CD pipeline
- Integrated GitHub repository with Jenkins
- Automated Docker image build using Jenkins pipeline
- Added Trivy security scanning stage in pipeline
- Automated Docker image push to Docker Hub
- Automated deployment using Docker Compose
- Fixed deployment issues (port conflict and container name mismatch)
- Handled Docker container cleanup during redeployment

---

## 🧱 Base Project

The original project already included:

- Flask backend application
- MySQL database integration
- Docker Compose setup for multi-container deployment
- Frontend UI for message submission

---

## ⚙️ Tech Stack

- Flask (Python)
- MySQL
- Docker & Docker Compose
- Jenkins (CI/CD)
- GitHub
- Trivy (Security scanning)

---

## 🔄 CI/CD Pipeline Flow

GitHub Push  
↓  
Jenkins Pipeline Trigger  
↓  
Checkout Source Code  
↓  
Build Docker Image  
↓  
Trivy Security Scan  
↓  
Push Image to Docker Hub  
↓  
Deploy using Docker Compose


---

## 🚀 Run Project Locally

```bash id="run1"
docker compose up -d --build

Stop:
```
docker compose down
🌐 Access Application

Frontend / Backend:
http://46.51.204.236:5000/

🗄️ Database Setup
CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);

---

⚠️ Notes
Base project was already built using Docker Compose
My work focused on CI/CD automation using Jenkins
Fixed runtime deployment issues (port conflict, container mismatch)

---

## 📸 Screenshots

### 🚀 Application Running

![App Running](https://raw.githubusercontent.com/ShahzaibGhaznavi/two-tier-flask-app/master/App-running.png)

### 🚀 Jenkins Stage View
![Jenkins Pipeline](https://raw.githubusercontent.com/ShahzaibGhaznavi/two-tier-flask-app/master/jenkins-pipeline.png)

### 🚀 Docker Container Running
![Docker Container](https://raw.githubusercontent.com/ShahzaibGhaznavi/two-tier-flask-app/master/docker-container.png)





