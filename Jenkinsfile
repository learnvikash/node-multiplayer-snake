node ('ubuntu') {
    def app
    
    stage('Cloning Git') {
        // This stage clones the source code from your Git repository
        checkout scm  // This checks out the source code as per Jenkins SCM configuration
    }

    stage('Build-and-Tag') {
        // This builds the Docker image from your Dockerfile
        app = docker.build("learnvikash/snake")  // Builds the image with the tag "learnvikash/snake"
    }

    stage('Post-to-dockerhub') {
        // This stage logs in to Docker Hub and pushes the image to the Docker registry
        docker.withRegistry('https://registry.hub.docker.com', 'learnvikash2') {
            app.push("new")  // Pushes the image with the tag "new"
        }
    }

    stage('Pull-image-server') {
        // This stage pulls down the Docker Compose stack and restarts it with the new image
        sh "docker-compose down"  // Shuts down the existing containers
        sh "docker-compose up -d"  // Brings up the containers in detached mode
    }
}

