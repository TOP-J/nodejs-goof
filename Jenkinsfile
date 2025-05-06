pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: 'origin/main']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          userRemoteConfigs: [[url: 'https://github.com/TOP-J/nodejs-goof.git']]])
            }
        }
        stage('Verify Node.js and Install Snyk CLI') {
            steps {
                sh 'node -v'
                sh 'npm -v'
                sh 'npm install -g snyk'
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
                sh 'curl -X GET "http://localhost:8090/JSON/ascan/action/scan/?url=http://localhost:3000"'
            }
        }
        // Add other stages here
    }
}
