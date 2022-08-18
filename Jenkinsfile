node {

    checkout scm
   def customImage = docker.build("mdshafi/nodejs") /* docker hub */

        /* Push the container to the custom Registry */
        customImage.push()
  docker.withRegistry('https://hub.docker.com', 'dockerhub')
    {

       
    }
  
}
