pipeline {
    agent {
        label 'base'
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    def customImage = docker.build('ibrashahin/my-mvcapp-image')
                    
                    // Push the Docker image to Docker Hub using Jenkins credentials
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerHub') {
                        customImage.push('latest')
                    }
                }
            }
        }
        
        stage('Run Docker Image') {
            steps {
                script {
                    // Run the Docker image as a container with automatic deletion after it stops
                    sh 'docker run -p 9000:8080 -p 9001:8081 --rm ibrashahin/my-mvcapp-image:latest'
                }
            }
        }
    }
}
