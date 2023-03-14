pipeline {
  environment {
    imagename = "farazzz/mlops"
    registryCredential = 'farazzz'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: 'master', credentialsId: 'farazamjad', url: 'https://github.com/farazamjad/Mlops_flaskEndpoint_Dockers.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build(imagename)
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry(registryCredential) {
            dockerImage.push("$BUILD_NUMBER")
            dockerImage.push('latest')
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
        sh "docker rmi $imagename:latest"
      }
    }
  }
}
