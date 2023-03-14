pipeline {
  agent any
  environment {
    DOCKER_REGISTRY = "docker pull farazzz/mlops"
    IMAGE_NAME = "model-image"
    IMAGE_TAG = "latest"
  }
  stages {
    stage('Build and Push Image') {
      steps {
        script {
          docker.withRegistry("${DOCKER_REGISTRY}", "docker-registry-credentials-id") {
            def dockerImage = docker.build("${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}", "-f Dockerfile .")
            dockerImage.push()
          }
        }
      }
    }
    stage('Create Container') {
      steps {
        script {
          docker.withRegistry("${DOCKER_REGISTRY}", "docker-registry-credentials-id") {
            def container = docker.run("${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}")
          }
        }
      }
    }
  }
}
