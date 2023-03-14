pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('faraz-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t model-image:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push image') {
        withDockerRegistry([ credentialsId: "faraz-dockerhub", url: "" ]) {
        bat "docker push model-image:latest"
        }
    }
  post {
    always {
      sh 'docker logout'
    }
  }
}