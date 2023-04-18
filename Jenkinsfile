pipeline {
  agent any

  environment {
    APP_NAME = 'my-python-app'
    ECR_REPO = 'my-ecr-repo'
    ECR_REGION = 'ap-southeast-1'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/omkarpatel00/my-python-app.git'
      }
    }
   stage('Logging into AWS ECR') {
      steps {
         script {
                  sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 305949049023.dkr.ecr.ap-south-1.amazonaws.com'
                }
            }
        }

    stage('Build') {
      steps {
        sh 'docker build -t my-ecr-repo-op .'
      }
    }

    stage('Push to ECR') {
      steps {
        script {
            sh "docker tag my-ecr-repo-op:latest 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com/my-ecr-repo-op:latest"
            sh "docker push 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com/my-ecr-repo-op:latest"
        }
      }
    }
  }
}
