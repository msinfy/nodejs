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
        
        stage('Deploy to  ...   aks') {
            steps{
                script{
             
                          
               withKubeConfig([credentialsId: 'k8s', serverUrl: 'https://aks-dns-9582e450.hcp.centralindia.azmk8s.io']) {
      sh 'kubectl apply -f aks.yaml'
                     }
               
               
                 }
              }
        }



    }

}
