pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
        timestamps()
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Verify Tools') {
            steps {
                bat 'git --version'
                bat 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t cloudops-portfolio:%BUILD_NUMBER% .'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Portfolio Docker image built successfully.'
        }
        failure {
            echo 'FAILED: Check the console output for the error.'
        }
    }
}
