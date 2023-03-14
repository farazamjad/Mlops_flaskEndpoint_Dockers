pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t model-image:latest .'
            }
        }
        stage('Run') {
            steps {
                sh 'docker run -d -p 5080:80 --name mycontainer model-imabe:latest'
            }
        }
    }

    post {
        always {
            sh 'docker stop mycontainer || true && docker rm mycontainer || true'
        }
    }
}
