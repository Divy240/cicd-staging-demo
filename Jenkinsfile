pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-staging-demo"
        CONTAINER_NAME = "staging-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Divy240/cicd-staging-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                bat "docker stop %CONTAINER_NAME% || exit 0"
                bat "docker rm %CONTAINER_NAME% || exit 0"
            }
        }

        stage('Deploy Container') {
            steps {
                bat "docker run -d -p 5000:5000 --name %CONTAINER_NAME% %IMAGE_NAME%:latest"
            }
        }

        stage('Test Deployment') {
            steps {
                bat "curl http://localhost:5000"
            }
        }
        stage('Test Docker') {
            steps {
                bat 'docker ps'
            }
        }
    }
}