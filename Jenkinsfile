
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t electronic-store:latest .'
            }
        }

        stage('Scan with Trivy') {
            steps {
                sh 'trivy image --exit-code 1 --severity HIGH,CRITICAL electronic-store:latest'
            }
        }

        stage('Deployment Preparation') {
            steps {
                echo 'Security scan passed. Ready for Docker Hub and Ansible deployment.'
            }
        }
    }

    post {
        success {
            echo 'Build and security scan completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
