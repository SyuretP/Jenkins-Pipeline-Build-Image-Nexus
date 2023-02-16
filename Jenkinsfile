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

    stage('login to nexus') {
      steps {
        sh 'docker login -u admin -p Letmein890!!!!! 143.42.61.152:8082'
      }
    }

    stage('push to nexus') {
      steps {
        sh '''docker push 143.42.61.152:8082/express:latest
'''
      }
    }

    stage('ssh to nexus server') {
      steps {
        sh 'ssh jenkins@143.42.61.152'
      }
    }

  }
}