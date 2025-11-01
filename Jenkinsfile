pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t hello-devops-jenkins .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5002:5000 --name hello-devops hello-devops-jenkins'
            }
        }
    }
    post {
        always {
            echo 'Current running containers:'
            sh 'docker ps -a'
        }
    }
}
