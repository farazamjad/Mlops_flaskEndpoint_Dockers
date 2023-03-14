pipeline {
    agent any
    environment {
        registry = "docker.io"
        registryCredential = 'faraz-dockerhub'
        imageName = "model-image"
        dockerImage = ''
    }
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build and Push Image') {
            environment {
                dockerImage = docker.build(imageName)
            }
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Create Container') {
            steps {
                sh "docker run -d -p 5080:80 --name mycontainer ${registry}/${imageName}:latest"
            }
        }
        stage('Run Tests') {
            steps {
                // Run tests against the container here
            }
        }
        stage('Cleanup') {
            steps {
                sh "docker stop mycontainer || true"
                sh "docker rm mycontainer || true"
            }
        }
    }
}
