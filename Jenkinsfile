pipeline { 

    environment { 

        registry = "mdshafi/nodejs" 

        registryCredential = 'dockerhub'

    }

    agent any 

    stages { 

        stage('Cloning our Git') { 

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

        stage ('K8S Deploy') {
        steps {
            script {
                kubernetesDeploy(
                    configs: 'gke.yaml',
                    kubeconfigId: 'k8s',
                    enableConfigSubstitution: true
                    )           
               
            }
        }
    }
        

    }

}
