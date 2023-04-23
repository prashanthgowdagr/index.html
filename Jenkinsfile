pipeline {
    agent any

    stages {
        stage('git pull') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/prashanthgowdagr/simple-index.html-app.git']])
            }
        }
        stage('Build and Publish Docker Image') {
            steps{
                script {
                    def imageTag = "pgrs/app:${env.BUILD_NUMBER}"
                    def latestTag = "pgrs/app:latest"
                    sh "docker build -t $imageTag -t $latestTag ."
                    withCredentials([usernamePassword(credentialsId: 'dockercreds', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh "docker stop my-app || true"
                        sh "docker rm my-app || true"
                        sh "docker run -d -p 80:80 --name my-app $latestTag"
                        sh "docker push $imageTag"
                        sh "docker push $latestTag"
                    }
                }
            }
        }
    }
}
