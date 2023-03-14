pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t myimage:latest .'
            }
        }
        stage('Run') {
            steps {
                sh 'docker run -d -p 8080:80 --name mycontainer myimage:latest'
            }
        }
    }

    post {
        always {
            sh 'docker stop mycontainer || true && docker rm mycontainer || true'
        }
    }
}
