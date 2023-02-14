pipeline {
  agent any
  stages {
    stage('Jenkinsfile') {
      steps {
        echo 'add file'
      }
    }

    stage('Checkout code') {
      steps {
        sh 'ls -la'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t express:latest -f Dockerfile .'
      }
    }

    stage('push to Nexus') {
      steps {
        sh 'docker push 143.42.61.152:8082/express:latest'
      }
    }

  }
}