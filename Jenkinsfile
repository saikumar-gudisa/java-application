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
                sh '''
              docker build . --tag web-app:latest
              docker tag web-app:latest a0alrhqhzjivs.jfrog.io/web-application/web-app:latest
                
                '''
                
            }
        }


       
      
    }
}
