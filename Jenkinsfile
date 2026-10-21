pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code is ready'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-ci-cd-app:latest .'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker image inspect my-ci-cd-app:latest'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker rm -f my-ci-cd-app || true'
                sh 'docker run -d --name my-ci-cd-app -p 8083:80 my-ci-cd-app:latest'
            }
        }
        stage('Smoke Test') {
            steps {
                sh 'curl -f http://localhost:8083/'
            }
        }
    }
}
