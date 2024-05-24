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
            step{
                git url: "${GIT_REPO_URL}", credentialsId: 'github-credentials'
            }

        }
        stage('build docker image'){
            step{
                dockerImage = docker.build(${DOCKER_IMAGE})
            }
        }
        stage('push docker image'){
            step{
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