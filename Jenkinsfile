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
                docker build . --tag web-application:latest
                docker tag web-application:latest saikumar/webapplication

                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'dockerhub_crdenatils', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
       
                    sh '''
                    docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD
                        docker push saikumargudisa/web-application:tagname

                    '''
                }
            } 
            
        }
   


        
       
        
    }
}
