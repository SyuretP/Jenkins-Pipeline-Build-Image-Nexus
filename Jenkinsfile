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
        NEXUS_PASSWORD = 'Letmein890!!!!!'
      }
      steps {
        sh 'docker login -u $NEXUS_USER -p $NEXUS_PASSWORD 143.42.61.152:8082'
      }
    }

    stage('push to nexus') {
      steps {
        sh '''docker push 143.42.61.152:8082/express:latest
'''
      }
    }

    stage('ssh to nexus server/pull docker image') {
      steps {
        sh '''#!/bin/bash


ssh -tt root@143.42.61.152 "docker pull 143.42.61.152:8082/express:latest && docker run -t -p 8085:8083 143.42.61.152:8082/express && docker ps -a -q --filter ancestor=143.42.61.152:8082/express | xargs docker rm && docker pull 143.42.61.152:8082/express:latest && docker run -t -d -p 8085:8083 143.42.61.152:8082/express" 

'''
      }
    }

    stage('Send email with status') {
      steps {
        mail(subject: 'Status', body: 'Check build status', from: 'Jenkins', to: 'syuretp89@gmail.com')
      }
    }

  }
}