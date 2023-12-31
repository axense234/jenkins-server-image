pipeline {
  agent any
  stages {
    stage('Setup') {
      steps {
        git(url: 'https://github.com/axense234/jenkins-server-image', branch: 'master')
      }
    }

    stage('NPM Test') {
      steps {
        sh 'npm --version'
      }
    }

    stage('AWS ECR Login') {
      steps {
        sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 797345446188.dkr.ecr.us-east-1.amazonaws.com'
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t private-jenkins-server-middle .'
      }
    }

    stage('AWS ECR Push') {
      steps {
        sh 'docker tag private-jenkins-server-middle:latest 797345446188.dkr.ecr.us-east-1.amazonaws.com/private-jenkins-server-middle:latest'
        sh 'docker push 797345446188.dkr.ecr.us-east-1.amazonaws.com/private-jenkins-server-middle:latest'
      }
    }

  }
}