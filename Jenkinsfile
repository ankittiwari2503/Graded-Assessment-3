pipeline {
  agent {
    label 'worker'
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
            sh 'cd node && sudo docker build . -t 437189082902.dkr.ecr.us-east-1.amazonaws.com/final_assignment:${BUILD_NUMBER}'
            sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 437189082902.dkr.ecr.us-east-1.amazonaws.com'
            sh 'sudo docker push 437189082902.dkr.ecr.us-east-1.amazonaws.com/final_assignment:${BUILD_NUMBER}'
          }
        }

             }
    }

    stage('Deploy in Docker') {
      steps {
        script {
          sh 'docker container run -itd -p 3000:3000 437189082902.dkr.ecr.us-east-1.amazonaws.com/final_assignment:${BUILD_NUMBER}'
        }

      }
    }
}
}
