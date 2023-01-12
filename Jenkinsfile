pipeline {
    agent any
    
      tools{
        
        dockerTool 'docker'
    }
    
  
    environment {
                 
            
        registry = "mdshafi/nodejs" 
        registryCredential = 'dockerhub'      
        CREDENTIALS_ID = 'k8s'

              }
    
     stages {
         
                  
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
         
       stage("Build image") {
            steps {
                script {
                    myapp = docker.build("mdshafi/nodejs:${env.BUILD_ID}")
                }
            }
        }
        
         stage('SonarQube analysis') {
                    //    def scannerHome = tool 'SonarScanner 4.8.0.2856';
            steps{
                   withSonarQubeEnv('sonarqube-4.8') { 
                   // If you have configured more than one global server connection, you can specify its name
                   //      sh "${scannerHome}/bin/sonar-scanner"
            sh "mvn sonar:sonar"
                 }
            }
        }
         
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            //myapp.push("${env.BUILD_ID}")
                    }
                }
            }
          }
        
      


    }

}
