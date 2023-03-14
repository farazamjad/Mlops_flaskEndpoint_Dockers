pipeline {
    agent {
        docker {
            image 'python:3.7'
            args '-u root'
        }
    }
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker image') {
            steps {
                sh 'docker build -t farazzz/mlops .'
            }
        }
        stage('Run container') {
            steps {
                sh 'docker run -p 5000:5000 farazzz/mlops'
            }
        }
    }
}
