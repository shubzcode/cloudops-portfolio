
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

        stage('Deploy Test Container') {
            steps {
                script {
                    bat(
                        returnStatus: true,
                        script: 'docker rm -f cloudops-portfolio-ci'
                    )
                }
                bat 'docker run -d --name cloudops-portfolio-ci -p 8083:80 cloudops-portfolio:%BUILD_NUMBER%'
            }
        }

        stage('Smoke Test') {
            steps {
                bat 'curl.exe -f http://localhost:8083/'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: CI build and test deployment completed.'
        }
        failure {
            echo 'FAILED: Check Console Output for details.'
        }
    }
}
