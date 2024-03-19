pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                echo "ini build"
                }
            }
        
        stage('Upload Image to DockerHub') {
            steps {
                echo "ini upload"
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
