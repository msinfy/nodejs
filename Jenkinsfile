pipeline {
    agent any
    environment {
      
        registry = "mdshafi/nodejs" 

        registryCredential = 'dockerhub'
        PROJECT_ID = 'ornate-serenity-355411'
        CLUSTER_NAME = 'autopilot-cluster-1'
        LOCATION = 'us-central1'
        CREDENTIALS_ID = 'gke'

    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        
        }
    }
}
