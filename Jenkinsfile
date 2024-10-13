pipeline {
    agent { label 'ahmedhakem' }
 
    environment {
        DOCKER_REGISTRY = 'https://hub.docker.com/u/ahmed10hakem?_gl=1*13ova4y*_gcl_au*OTEyMDE4MDU5LjE3MjE3NTU3MzQ.*_ga*MTMwNDY1MzgzNS4xNzIwODAzNjc4*_ga_XJWPQMJYHQ*MTcyODg0Mjk1Ny4yNi4xLjE3Mjg4NDUyMjkuNTkuMC4w'
        IMAGE_NAME = 'spring-mvnc'
        TAG = 'latest'  // You can replace this with a version or commit hash
    }

     stages {
        stage('Checkout') {
            steps {
                // Checkout code from your source repository
                git branch: 'main', url: 'https://github.com/ahmedabdelhakim13/spring-mvc.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                       sh "docker build -t ${IMAGE_NAME}:${TAG} ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                // Login to Docker registry
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'docker-credentials') {
                        // Push the image to Docker registry
                        docker.image("${IMAGE_NAME}:${TAG}").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Example deployment step (adjust for your environment)
                echo "Deploying the image ${IMAGE_NAME}:${TAG} to the environment..."
            }
        }
    }

    post {
        always {
            // Clean up after the build
            cleanWs()
        }
    }
}      
