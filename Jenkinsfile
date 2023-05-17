pipeline{
    agent any
    stages{
        stage('checkout code'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sreenumarolix/nodejs-cicd-main.git']] )
            }
        }
        stage('Build docker image'){
            steps{
             script{
                 sh 'docker build -t image1:1.0 .'
             }   
            }
        }
        stage('create docker container'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'sreenu12', variable: 'sreenu12')]) {
                        sh 'docker login -u msreenu -p ${sreenu12}'
                    }
                       sh 'docker tag image1:1.0 msreenu/docker2:1.0'
                       sh 'docker push msreenu/docker2:1.0'
                       sh 'docker run -d -p 3000:3000 image1:1.0 npm start'
                }
            }
        }
    }
}
