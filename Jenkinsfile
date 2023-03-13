pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY = "https://registry.hub.docker.com"
        IMAGE_NAME = "farazamjad/model-image"
        IMAGE_TAG = "latest"
    }
    
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker image') {
            steps {
                script {
                    docker.build("${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }
        
        stage('Run container') {
            steps {
                script {
                    docker.withRegistry("${DOCKER_REGISTRY}", "dockerhub_creds") {
                        docker.image("${DOCKER_REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG}").run("-p 5000:5000 --name model-image -d")
                    }
                }
            }
        }
    }
}
