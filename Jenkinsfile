pipeline {
    agent any
    
    
   
    
    environment {
             
        def dockerHome = tool 'docker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
        
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

        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
          }
        
      


    }

}
