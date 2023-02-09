pipeline {
    agent any
            tools {
                nodejs 'node'
            }
            yaml '''
apiVersion: v1 
kind: Pod
spec:
  containers:
  - name: shell
    image: ubuntu
    command:
    - sleep
    args:
    - infinity
  - name: docker
    env:
    - name: DOCKER_HOST
      value: 127.0.0.1
    image: docker
    command:
    - cat
    tty: true
'''
            // Can also wrap individual steps:
            // container('shell') {
            //     sh 'hostname'
            // }
            defaultContainer 'shell'
        }
    }
    stages {
        
        stage('example') {
            steps {
                //sh 'npm install'
                sh 'npm version'
            }
        }

        stage('Image Build') {
          environment {
            DOCKERHUB_CREDS = credentials('dockerhub')
         }
        steps {
          container('docker') {
           sh "docker build -t shtlamrut/kubenode-demo:${env.GIT_COMMIT} ."
           sh "docker login --username $DOCKERHUB_CREDS_USR --password $DOCKERHUB_CREDS_PSW" 
           sh "docker push shtlamrut/kubenode-demo:${env.GIT_COMMIT}"
        }
      }
    }
        stage('Main') {
            steps {
                sh 'hostname'
            }
        }
    }

