pipeline{

    agent any


    enviroment{
        DOCKERHUB_CREDENTIALS = 'dockerhub-credentials'
        DOCKER_IMAGE = 'khanjanpurani307/hello-world'
        REGISTRY_CREDENTIALS == dockerhub
        GIT_REPO_URL = 'https://github.com/Khanjanpurani/Jenkins-pipeline-with-docker.git'

    }

    stages{
        stage('checkout'){
            steps{
                git url: "${GIT_REPO_URL}", credentialsId: 'github-credentials'
            }

        }
        stage('build docker image'){
            steps{
                dockerImage = docker.build(${DOCKER_IMAGE})
            }
        }
        stage('push docker image'){
            steps{
                docker.withRegistry('',"${DOCKERHUB_CREDENTIALS}"){
                    dockerImage.push('latest')
                }
            }
        }
        stage('deploy container'){
            script{
                sh 'docker run -d --name hello-world-app -p 8080:80 ${DOCKER_IMAGE}'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
