pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('iccp-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/iccpnorthindia/docker-feb2024project.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t iccpinfotech/iccpwebimage:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push iccpinfotech/iccpwebimage:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
