node {

    checkout scm

    docker.withRegistry('https://hub.docker.com', 'dockerhub') {

        def customImage = docker.build("mdshafi/nodejs") /* docker hub */

        /* Push the container to the custom Registry */
        customImage.push()
    }
}
