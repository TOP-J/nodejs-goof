pipeline {
    agent any
    tools {
        nodejs 'NodeJS 18' // Replace 'NodeJS 18' with the exact name of your configured Node.js installation in Jenkins (in Global Tool Configuration)
    }
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
        stage('Install Snyk CLI') {
            steps {
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
        // Add other stages here (e.g., for Falco monitoring setup if needed)
    }
}
