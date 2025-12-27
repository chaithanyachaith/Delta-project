Django CI Pipeline with Docker & Jenkins 🚀

A complete CI automation project that demonstrates how to build, containerize, and publish a Django application using Docker and Jenkins, with source code hosted on GitHub and images pushed to Docker Hub.

📌 Project Objective

To automate the following workflow:
Pull source code from GitHub
Build a Docker image for a Django application
Push the Docker image to Docker Hub
Achieve a repeatable and production-style CI process

🔄 CI Workflow (High-Level)

Developer
   |
   v
GitHub Repository
   |
   v
Jenkins Pipeline
   |
   ├── Checkout Code
   ├── Build Docker Image
   └── Push Image to Docker Hub

🏗 Architecture Diagram
+------------+        +-------------+        +-------------+
|  Developer | -----> |   GitHub     | -----> |   Jenkins   |
+------------+        +-------------+        +-------------+
                                                |
                                                v
                                         +-------------+
                                         |   Docker    |
                                         |  Image Build|
                                         +-------------+
                                                |
                                                v
                                         +-------------+
                                         | Docker Hub  |
                                         |  Repository |
                                         +-------------+

🧰 Tech Stack

Language: Python 3.11
Framework: Django
Containerization: Docker
CI Tool: Jenkins (Declarative Pipeline)
Registry: Docker Hub
Source Control: GitHub

📁 Project Structure

.
├── Dockerfile
├── Jenkinsfile
├── requirements.txt
├── manage.py
├── db.sqlite3
├── DELTA/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
└── DL_Term/


🐳 Docker Implementation
Key confirms:

Uses python:3.11-slim for smaller image size
Installs only required system packages
Dependencies installed via requirements.txt
Django app exposed on port 8000
Build Image Locally
docker build -t django-delta .

Run Container
docker run -p 8000:8000 django-delta

⚙ Jenkins Pipeline Flow (Detailed)
Pipeline Start
     |
     v
Checkout Code (GitHub)
     |
     v
Docker Build Stage
     |
     v
Authenticate with Docker Hub
     |
     v
Push Image to Docker Hub
     |
     v
Pipeline Complete

🧪 Jenkinsfile Overview
Environment Configuration
environment {
    DOCKERHUB_USERNAME = "chaithanya7995"
    DOCKERHUB_REPO = "django-images"
    DOCKERHUB_CREDENTIALS = "docker-hub-credentials"
}


Docker Hub credentials are securely stored in Jenkins Credentials Manager.

Jenkins Pipeline Stages
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/chaithanyachaith/Delta-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_USERNAME}/${DOCKERHUB_REPO}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry(
                        'https://index.docker.io/v1/',
                        DOCKERHUB_CREDENTIALS
                    ) {
                        docker.image(
                          "${DOCKERHUB_USERNAME}/${DOCKERHUB_REPO}:latest"
                        ).push()
                    }
                }
            }
        }
    }
}

📦 Docker Hub Output

Repository: chaithanya7995/django-images

Tags:
latest
Jenkins build-based tags (optional improvement)
Pull Image
docker pull chaithanya7995/django-images:latest

🌐 Application Access

Once the container is running:

http://localhost:8000

✅ Achievements

✔ Dockerized Django application
✔ Optimized Docker image size
✔ Implemented Jenkins CI pipeline
✔ Secure credential handling
✔ Automated image publishing
✔ Production-style workflow

🚀 Future Enhancements

GitHub Webhooks for auto-triggered builds
Multi-stage Docker builds
Add testing stage in Jenkins
Push image tags using Git commit hash
Deploy to Kubernetes (EKS / AKS / GKE)

👨‍💻 Author

Chaithanya

DevOps & Cloud Enthusiast

GitHub: https://github.com/chaithanyachaith
