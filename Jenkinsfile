pipeline{
    agent any
    stages{
        stage('checkout code'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/veeraboinaashok/nodejs-cicd-main.git']] )
            }
        }
        stage('Build docker image'){
            steps{
             script{
                 sh 'docker build -t ashok:0.2 .'
             }   
            }
        }
        stage('create docker container'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerpasswd', variable: 'dockerpasswd')]) {
                        sh 'docker login -u veeraboinaashok0124 -p ${dockerpasswd}'
                    }
                       sh 'docker tag  ashok:0.2 veeraboinaashok0124/ashokk:0.2'
                       sh 'docker push veeraboinaashok0124/ashokk:0.2'
                       sh ' docker run -d -p 3000:3000 ashok:0.2 npm start'
                }
            }
        }
    }
}