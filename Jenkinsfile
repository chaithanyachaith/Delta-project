pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'docker-hub-credentials'
        DOCKERHUB_USERNAME   = 'chaithanya7995'
        IMAGE_REPO           = 'django-images'
        IMAGE_TAG            = 'latest'
        FULL_IMAGE_NAME      = "${DOCKERHUB_USERNAME}/${IMAGE_REPO}:${IMAGE_TAG}"
    }

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
                    docker.build(FULL_IMAGE_NAME)
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
                        docker.image(FULL_IMAGE_NAME).push()
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
