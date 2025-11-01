pipeline {
    agent any

    environment {
        IMAGE_NAME = 'hello-devops-jenkins'
        CONTAINER_NAME = 'hello-devops'
        HOST_PORT = '5001'
        CONTAINER_PORT = '5000'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/gk-maker0105/empty'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running container...'
                sh """
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                    docker run -d -p ${HOST_PORT}:${CONTAINER_PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}
                """
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
