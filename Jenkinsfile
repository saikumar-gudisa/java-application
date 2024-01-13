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



        stage('Build Docker Image') {
            steps {
                script {
                    // Define your Docker image name and tag
                    def dockerImage = 'saikumargudisa/web-application:latest'

                    // Build the Docker image
                    sh "docker build -t $dockerImage ."
                }
            }
        }



       
      
    }
}
