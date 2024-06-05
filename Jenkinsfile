pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS_ID = '1'
        IMAGE_TAG = "latest"
    }
    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Install dependencies for each microservice
                    dir('Auth') {
                        bat 'npm install'
                    }
                    dir('Classrooms') {
                        bat 'npm install'
                    }
                    dir('Event-Bus') {
                        bat 'npm install'
                    }
                    dir('Post') {
                        bat 'npm install'
                    }
                    dir('Client') {
                        bat 'npm install'
                    }
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    docker.build("afnannaseem837/auth:${IMAGE_TAG}", "./Auth").push()
                    docker.build("afnannaseem837/classrooms:${IMAGE_TAG}", "./Classrooms").push()
                    docker.build("afnannaseem837/event-bus:${IMAGE_TAG}", "./Event-Bus").push()
                    docker.build("afnannaseem837/post:${IMAGE_TAG}", "./Post").push()
                    docker.build("afnannaseem837/client:${IMAGE_TAG}", "./Client").push()
                }
            }
        }
        stage('Test with Docker Compose') {
            steps {
                script {
                    // Start services with Docker Compose
                    bat 'docker-compose up -d'
                    
                    // Run some tests to ensure services are working
                    // You can add test scripts here if needed

                    // Stop services after testing
                    bat 'docker-compose down'
                }
            }
        }
    }
    post {
        always {
            script {
                // Clean up unused Docker images to save space
                bat 'docker image prune -f'
            }
        }
    }
}
