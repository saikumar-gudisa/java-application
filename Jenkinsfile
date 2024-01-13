pipeline {
    agent any

    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    docker.image('docker:dind').inside('-u root') {
                        // Your Docker commands go here
                        sh 'docker build -t web-application:latest .'
                    }
                }
            }
        }
    }
}
