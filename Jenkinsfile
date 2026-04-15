pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-staging-demo"
        CONTAINER_NAME = "staging-container"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Divy240/cicd-staging-demo.git'
            }
        }

        stage('Build Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Stop Old Container') {
            steps {
                bat "docker stop %CONTAINER_NAME% || exit 0"
                bat "docker rm %CONTAINER_NAME% || exit 0"
            }
        }

        stage('Run Container') {
            steps {
                bat "docker run -d -p 5000:5000 --name %CONTAINER_NAME% %IMAGE_NAME%"
            }
        }

        stage('Check') {
            steps {
                bat "docker ps"
            }
        }
    }
}