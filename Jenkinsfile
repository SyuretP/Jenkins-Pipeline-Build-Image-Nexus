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
      environment {
        NEXUS_USER = 'admin'
        NEXUS_PASSWORD = 'changeme'
      }
      steps {
        sh 'docker login -u $NEXUS_USER -p $NEXUS_PASSWORD localhost:8082'
      }
    }

    stage('push to nexus') {
      steps {
        sh '''docker push localhost:8082/express:latest
'''
      }
    }

    stage('ssh to nexus server/pull docker image') {
      steps {
        sh '''#!/bin/bash


ssh -tt root@localhost "docker pull localhost:8082/express:latest && docker run -t -p 8085:8083 localhost:8082/express && docker ps -a -q --filter ancestor=localhost:8082/express | xargs docker rm && docker pull localhost:8082/express:latest && docker run -t -d -p 8085:8083 localhost:8082/express" 

'''
      }
    }

    stage('Send status email') {
      steps {
        emailext(subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', body: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:  Check console output at $BUILD_URL to view the results.', from: 'Jenkins', to: 'syuretp89@gmail.com', attachLog: true)
      }
    }

  }
}
