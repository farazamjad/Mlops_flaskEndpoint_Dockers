 pipeline {
    agent any
    stages {
        stage('Build Docker image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', '') {
                        def customImage = docker.build("model-image:${env.BUILD_ID}")
                        customImage.push()
                    }
                }
            }
        }
        stage('Run container') {
            steps {
                sh 'docker run -d -p 5000:5000 model-image:${env.BUILD_ID}'
            }
        }
    }
}
