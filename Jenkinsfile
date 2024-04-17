pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the GitHub repository
                git 'https://github.com/ibrahim-shahin/MVCapp.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    def customImage = docker.build('my-mvcapp-image')
                    
                    // Push the Docker image to Docker Hub using Jenkins credentials
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerHub') {
                        customImage.push('latest')
                    }
                }
            }
        }
        
        stage('Run Docker Image') {
            steps {
                // Run the Docker image as a container
                script {
                    docker.image('my-mvcapp-image').run('-p 9000:8080', '-p 9001:8081', '--rm')
                }
            }
        }
    }
}
