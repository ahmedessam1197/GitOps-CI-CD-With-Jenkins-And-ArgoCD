pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-reg'       
        IMAGE_NAME = 'ahmed277/jenkins-nodejs:latest'  
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ahmedessam1197/GitOps-CI-CD-With-Jenkins-And-ArgoCD'
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    echo 'Logging in to Docker Hub...'
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        echo 'Login successful'
                    }
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    def app = docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    echo 'Pushing image to Docker Hub...'
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        def app = docker.image("${IMAGE_NAME}")
                        app.push('latest')
                    }
                }
            }
        }
    }
}
