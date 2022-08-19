pipeline {
     agent {
         label 'myslave'
     }
        environment {
        //once you sign up for Docker hub, use that user_id here
        registry = "mdshafi/nodejs"
        //- update your credentials ID after creating credentials for connecting to Docker Hub
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    stages {

        stage ('checkout') {
            steps {
            checkout SCM
            }
        }
       
        stage ('Build docker image') {
            steps {
                script {
                dockerImage = docker.build registry
                }
            }
        }
       
         
    }
    
}
