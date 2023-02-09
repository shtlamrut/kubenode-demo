pipeline {
    agent any
    tools {
        nodejs 'node'
    }
    stages {
        stage('Build') {
            steps {
               // sh 'nodejs --version'
                sh 'npm install'
                sh 'npm test'
            }
        }
        stage('Test') {
            steps {
                sh 'npm --version'
                
            }
        }
    }
}
