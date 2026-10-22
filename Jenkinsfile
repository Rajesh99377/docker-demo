
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
        sh 'docker rm -f my-ci-cd-app-ci || true'
        sh 'docker run -d --name my-ci-cd-app-ci -p 8083:80 my-ci-cd-app:latest'
        sh 'docker network connect devops-network my-ci-cd-app-ci'
    }
}

stage('Smoke Test') {
    steps {
        sh 'curl -f --max-time 10 http://my-ci-cd-app-ci/'
    }
}
    }
}
