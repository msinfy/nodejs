pipeline { 

    environment { 

        registry = "mdshafi/nodejs" 

        registryCredential = 'dockerhub'

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


    }

}
        
