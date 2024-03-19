pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'kalax1011/personal-website'
    }
    stages {
        stage('Delete Old Image') {
            steps {
                script {
                    // Delete old Docker image if it exists
                    sh "docker rmi -f ${DOCKER_IMAGE} || true"
                }
            }
        }

        stage('Build Image') {
            steps {
                // Build Docker image
                script {
                    //sh "docker build -t ${DOCKER_IMAGE} ."
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Upload Image to DockerHub') {
            steps {
            script {
                    // Login to Docker Hub
                    withDockerRegistry([credentialsId: 'your_dockerhub_credential_id', url: 'https://index.docker.io/v1/']) {
                        // Push Docker image to Docker Hub
                        docker.image("${DOCKER_IMAGE}").push("latest")
                    }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded! Docker image built and pushed.'
        }
        failure {
            echo 'Pipeline failed! Handle errors if needed.'
        }
    }
}