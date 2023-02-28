pipeline {
  agent {
    label 'upgrad'
  }
  stages {
    stage('Git Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      parallel {
        stage('Build Docker Image') {
          steps {
            sh 'cd node && sudo docker build . -t 437189082902.dkr.ecr.us-east-1.amazonaws.com/node:${BUILD_NUMBER}'
            sh 'sudo docker push 437189082902.dkr.ecr.us-east-1.amazonaws.com/node:${BUILD_NUMBER}'
          }
        }

             }
    }
