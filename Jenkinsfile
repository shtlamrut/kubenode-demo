pipeline {
    agent any
    tools{
        nodejs 'node'
    }

    stages {
        stage('example') {
            steps {
                //sh 'npm install'
                sh 'npm version'
            }
        }
    }
}
