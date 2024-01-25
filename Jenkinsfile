pipeline {
    agent any

    tools{
        maven "Maven 3.9.6"
    }
    
    stages {

        stage('Clone the repository'){
        steps{
          
            git branch: 'pushing-docker-image-to-ecr-jenkinsfile', credentialsId: 'Github_credentails', url: 'https://github.com/saikumar-gudisa/java-application.git'
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
              docker tag web-application:$BUILD_NUMBER 742725064771.dkr.ecr.us-east-1.amazonaws.com/web-application:$BUILD_NUMBER
                
                '''
                
            }
        }  

        stage('Push Docker Image') {
           withAWS(credentials: 'AWS', region: 'us-east-1') {

               sh '''
               aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 742725064771.dkr.ecr.us-east-1.amazonaws.com
               docker push 742725064771.dkr.ecr.us-east-1.amazonaws.com/web-application:$BUILD_NUMBER
}
        }  

        

  
     

        
   
        
    }
}
