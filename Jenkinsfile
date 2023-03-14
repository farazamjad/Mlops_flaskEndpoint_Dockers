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
        sh 'docker build -t model-image:first .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push Docker Image') {
      steps {
        withDockerRegistry([credentialsId: "faraz-dockerhub", url: "https://index.docker.io/v1/"]) {
          sh  "docker push farazzz/mlops1:first"
                }
            }
        }
      }

  post {
    always {
      sh 'docker logout'
    }
  }
}