pipeline {
    agent any
    tools{
        maven "Maven 3.9.6"
    }
    stages {
      stage('Clone the repository'){
        steps{
          git branch: 'pushing-docker-image-to-dockerhub-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/saikumar-gudisa/java-application.git'
          
        } 
      }

stage('Build the code') {
            steps {
                sh 'mvn clean install'
            }
        }


        
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
