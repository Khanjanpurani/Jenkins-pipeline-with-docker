pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'
        DOCKER_IMAGE = 'khanjanpurani307/hello-world'
        REGISTRY_CREDENTIALS = 'dockerhub'
        GIT_REPO_URL = 'https://github.com/Khanjanpurani/Jenkins-pipeline-with-docker.git'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: "${GIT_REPO_URL}", credentialsId: 'github-credentials'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_CREDENTIALS_ID}") {
                        dockerImage.push('latest')
                    }
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    sh 'docker run -d --name hello-world-app -p 8080:80 ${DOCKER_IMAGE}'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
