node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        def customImage = docker.build("mdshafi/nodejs/") 
    }

   
}
