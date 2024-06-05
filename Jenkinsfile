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
