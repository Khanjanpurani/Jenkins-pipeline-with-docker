pipeline {
    agent any

    environment {
        
        GITHUB_CREDENTIALS_ID = 'github-credentials'  
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'  
        DOCKER_IMAGE = 'Khanjanpurani/hello-world-app'  
    }

    stages {
        stage('Checkout') {
            steps {
                
                git credentialsId: "${GITHUB_CREDENTIALS_ID}", url: 'https://github.com/Khanjanpurani/Jenkins-pipeline-with-docker'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}").push('latest')
                    }
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                  
                    sh "docker run -d --name hello-world-container ${DOCKER_IMAGE}:latest"
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
