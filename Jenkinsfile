pipeline {
    agent any
    tools{
        docker 'Docker'
    }

    stages {
        stage('Build Image') {
            steps {
                sh docker build -t kalax1011/personal-website
                //docker run kalax1011/personal-website
                
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
