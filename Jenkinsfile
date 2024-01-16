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
                docker build . --tag web-application:$BUILD_NUMBER
                docker tag web-application:$BUILD_NUMBER saikumargudisa/web-application:$BUILD_NUMBER

                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'Dockerhub-username-password', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                      sh '''
                      docker login -u $DOCKERHUB_USERNAME  -p $DOCKERHUB_PASSWORD
                      docker push saikumargudisa/webapplication:$BUILD_NUMBER


                      
                      '''
                  }
            } 
            
        }
   
        
    }
}
