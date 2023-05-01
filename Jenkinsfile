pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('tanishkagoyanka-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/s-shr05/devops-project.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t tanishkagoyanka/Eshop:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push tanishkagoyanka/Eshop:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
