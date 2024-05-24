pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository using credentials
                git url: 'https://github.com/Khanjanpurani/Jenkins-pipeline-with-docker.git', credentialsId: 'github-credentials', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('your-image-name:latest')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('your-image-name:latest').push()
                    }
                }
            }
        }
        stage('Deploy Docker Container') {
            steps {
                script {
                    docker.run('your-image-name:latest', '-d -p 8080:8080')
                }
            }
        }
    }
}
