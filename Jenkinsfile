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
        stage('Deploy to GKE') {
            steps{
                
                //gke
                //step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'gke.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
                
                #aks
                script{
                        kubernetesDeploy(configs: 'aks.yaml', kubeconfigId: 'K8S', enableConfigSubstitution: true )                    
                }
                
                
                
            }
        }
    }
}
