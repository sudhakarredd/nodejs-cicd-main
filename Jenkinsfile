pipeline{
    agent any
    stages{
        stage('checkout code'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sudhakarredd/nodejs-cicd-main.git']])
            }
        }
        stage('Build docker image'){
            steps{
             script{
                 sh 'docker build -t image1:2.0 .'
             }   
            }
        }
        stage('create docker container'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'sudhakarred1', variable: 'dockerhub')]) {
                        sh 'docker login -u sudhakarred1 -p ${dockerhub}'
                    }
                       sh 'docker tag  image1:2.0 sudhakarred1/dockerhub:2.0'
                       sh 'docker push sudhakarred1/dockerhub:2.0'
                       sh 'docker run -d -p 3000:3000 image1:2.0 npm start'
                }
            }
        }
    }
}
