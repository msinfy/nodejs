pipeline { 

    environment { 

        registry = "mdshafi/nodejs" 

        registryCredential = 'dockerhub'
        PROJECT_ID = 'ornate-serenity-355411'
        CLUSTER_NAME = 'autopilot-cluster-1'
        LOCATION = 'us-central1'
        CREDENTIALS_ID = 'gke'

                 }

    agent any 

    stages { 

        stage('Cloning our Git checkout') { 

            steps { 

                git 'https://github.com/msinfy/nodejs.git' 

                   }

                                } 

        stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }

        stage('Deploy our image') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                    }

                } 

            }

        } 
        
        
       stage('Deploy to GKE') {
            steps{
                sh "sed -i 's/nodejs:latest/nodejs:${env.BUILD_ID}/g' gke.yaml"
                step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
        }
           
       }
               
        
      
        
        
        


    }

}
        
