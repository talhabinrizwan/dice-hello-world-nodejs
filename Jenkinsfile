pipeline {
    agent any
    environment {
      registryCredentials = 'dockerhub'
    }
    stages {
        stage('Build') {
            steps {
              sh 'docker build -t talhabinrizwan/test-node-app .'
            }
        }
        stage('Test') {
            steps {
              sh 'docker container rm -f node || true'
              sh 'docker container run -p 8001:8080 --name node -d talhabinrizwan/test-node-app'
              sh 'curl -I http://localhost:8001'
            }
        }
        stage('Publish') {
            steps {
              script {
                docker.withRegistry('', registryCredentials) {
                  sh 'docker push talhabinrizwan/test-node-app:latest'
                }
              }
            }
        }
    }
}
