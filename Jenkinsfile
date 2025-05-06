pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/TOP-J/nodejs-goof.git'
            }
        }
        stage('Snyk Test') {
            steps {
                sh 'snyk test'
            }
        }
        stage('Trivy Scan') {
            steps {
                sh 'docker build -t myapp:latest .'
                sh 'trivy image myapp:latest'
            }
        }
        stage('ZAP Scan') {
            steps {
                sh 'curl -X GET "http://localhost:8090/JSON/ascan/action/scan/?url=http://localhost:3000"' // Adjust the URL as needed
            }
        }
        // You can add more stages here for Falco or other steps
    }
}
