pipeline {
    agent any

    environment {
        IMAGE_NAME = "django-delta"
        DOCKERHUB_CREDENTIALS = "docker-hub-credentials" // Jenkins credential ID
        DOCKERHUB_USERNAME = "chaithanya7995"
        DOCKERHUB_REPO = "django-images"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/chaithanyachaith/Delta-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKERHUB_USERNAME}/${DOCKERHUB_REPO}:latest:${IMAGE_TAG}")
                }
            }
        }

        
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS}") {
                        docker.image("${DOCKERHUB_USERNAME}/${DOCKERHUB_REPO}:latest:${IMAGE_TAG}").push()
                        docker.image("${DOCKERHUB_USERNAME}/${DOCKERHUB_REPO}:latest:${IMAGE_TAG}").push("latest")
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}