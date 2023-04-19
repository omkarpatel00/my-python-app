pipeline {
  agent any

  environment {
    APP_NAME = 'my-python-app'
    ECR_REPO = 'my-ecr-repo'
    ECR_REGION = 'ap-southeast-1'
  }

  stages {
    stage('Clone Repo') {
        steps {
		checkout([$class: 'GitSCM', branches: [[name: '*/master']],
		doGenerateSubmoduleConfigurations: true, extensions: [],
		submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'omkarpatel00',
		url: 'https://github.com/omkarpatel00/my-python-app.git']]])
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
	    sh "aws ecr get-login --region ap-southeast-1"
            sh "docker tag my-ecr-repo-op:latest 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com/my-ecr-repo-op:latest"
            sh "docker push 490167669940.dkr.ecr.ap-southeast-1.amazonaws.com/my-ecr-repo-op:latest"
        }
      }
    }
  }
}
