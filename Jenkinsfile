pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build using Maven') {
      steps {
        bat 'docker build -t ArpitaSin/jenkins-docker .'
      }
    }
    stage('Login to Docker Hub') {
      steps {
        bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push to Docker Hub') {
      steps {
        bat 'docker push ArpitaSin/jenkins-docker'
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}
