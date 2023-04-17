pipeline {
  agent any

  environment {
    APP_NAME = 'my-python-app'
    ECR_REPO = 'my-ecr-repo'
    ECR_REGION = 'us-east-1'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/your-github-username/my-python-app.git'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t $APP_NAME .'
      }
    }

    stage('Push to ECR') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
          sh "aws ecr get-login-password --region $ECR_REGION | docker login --username AWS --password-stdin $ECR_REPO"
          sh "docker tag $APP_NAME:latest $ECR_REPO/$APP_NAME:latest"
          sh "docker push $ECR_REPO/$APP_NAME:latest"
        }
      }
    }
  }
}
