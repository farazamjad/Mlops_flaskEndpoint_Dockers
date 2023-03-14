pipeline {
  environment {
    registry = "https://hub.docker.com"
    registryCredential = 'farazzz/faraz121,.'
    imageName = "model-image"
    dockerImageTag = "latest"
  }
  agent any
  
    
    stage('Building Docker Image') {
      steps {
        script {
          dockerImage = docker.build("${registry}/${imageName}:${dockerImageTag}", "-f Dockerfile .")
        }
      }
    }
    stage('Push Docker Image') {
      steps {
        script {
          docker.withRegistry( "${registry}", registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Deploy to Container') {
      steps {
        script {
          docker.image("${registry}/${imageName}:${dockerImageTag}").run("-p 5000:5000 --name ${imageName}")
        }
      }
    }
  }
}
