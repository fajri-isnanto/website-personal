pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'personal-website'
    }
    tools {
        // Define Docker tool
        docker 'Docker'
    }

    stages {
        stage('Build Image') {
            steps {
                // Build Docker image
                script {
                    sh "docker build -t ${DOCKER_IMAGE} ."
                }
            }
        }

        stage('Upload Image to DockerHub') {
            steps {
                // Here you would push the image to DockerHub, replace this echo statement with your actual Docker push command
                echo "Upload to DockerHub"
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