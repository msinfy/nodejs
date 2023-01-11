pipeline {
    agent any
    environment {
      
        def dockerHome = tool 'docker'
       
        registry = "mdshafi/nodejs" 

        registryCredential = 'docker'
      
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
                    docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
          }
        
      


    }

}
