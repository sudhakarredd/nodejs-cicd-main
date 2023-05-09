pipeline{
    agent any
    stages{
        stage('checkout code'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bvenkydevops/nodejs-cicd-main']])
            }
        }
        stage('Build docker image'){
            steps{
             script{
                 sh 'docker build -t venky:2.0 .'
             }   
            }
        }
        stage('create docker container'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
                        sh 'docker login -u bojjavenkatesh -p ${dockerhub}'
                    }
                       sh 'docker tag  venky:2.0 bojjavenkatesh/cicd-node:0.2'
                       sh 'docker push bojjavenkatesh/cicd-node:0.2'
                       sh ' docker run -d -p 3000:3000 nodejs-cicd npm start'
                }
            }
        }
    }
}
