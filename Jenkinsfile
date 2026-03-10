pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/munigondavijay-oss/train-ticket-reservation.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t train-ticket-reservation:v1 .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker stop train-app || true'
                sh 'docker rm train-app || true'
                sh 'docker run -d -p 8081:8080 --name train-app train-ticket-reservation:v1'
            }
        }
    }
}
