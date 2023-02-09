pipeline {
    agent any
    tools {
        nodejs 'node'
    }
yaml """    
apiVersion: v1
kind: Pod
spec:
  containers:
   - name: docker
    env:
    - name: DOCKER_HOST
      value: 127.0.0.1
    image: docker
    command:
    - cat
    tty: true    
  """
    
    stages {
       /* stage('Build') {
            steps {
               // sh 'nodejs --version'
                //sh 'npm install'
                //sh 'npm test'
            }
        }*/
        stage('Image Build') {
        environment {
        DOCKERHUB_CREDS = credentials('demo-docker')
      }
      steps {
        container('docker') {
          sh "docker build -t shtlamrut/kubenode-demo:${env.GIT_COMMIT} ."
          sh "docker login --username $DOCKERHUB_CREDS_USR --password $DOCKERHUB_CREDS_PSW" 
          sh "docker push shtlamrut/kubenode-demo:${env.GIT_COMMIT}"
        }
      }
    }

        stage('Test') {
            steps {
                sh 'npm --version'
                
            }
        }
    }
}
