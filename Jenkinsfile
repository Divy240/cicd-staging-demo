pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/Divy240/cicd-staging-demo.git'
            }
        }

        stage('Build Images') {
            steps {
                bat 'docker compose build'
            }
        }

        stage('Run Containers') {
            steps {
                bat 'docker compose up -d'
            }
        }

        stage('Verify') {
            steps {
                bat 'docker ps'
            }
        }
    }
}