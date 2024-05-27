pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        DOCKER_IMAGE = 'puranikhanjan307/python-hello-world'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Khanjanpurani/Jenkins-pipeline-with-docker.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        docker.image(DOCKER_IMAGE).push("latest")
                    }
                }
            }
        }
        
        stage('Deploy Docker Container') {
            steps {
                script {
                    sh """
                        docker pull ${DOCKER_IMAGE}:latest
                        docker run -d --name hello-world-app ${DOCKER_IMAGE}:latest
                    """
                }
            }
        }
    }
}
