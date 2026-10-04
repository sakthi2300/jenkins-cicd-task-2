pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t jenkins-cicd-task-2:latest .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                bat 'docker run --rm jenkins-cicd-task-2:latest node --check server.js'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                bat 'docker rm -f jenkins-cicd-task-2 >nul 2>&1 || exit /b 0'
                bat 'docker run -d -p 3000:3000 --name jenkins-cicd-task-2 jenkins-cicd-task-2:latest'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}