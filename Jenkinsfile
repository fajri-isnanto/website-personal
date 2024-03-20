pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('kalax1011')
        DOCKER_IMAGE = 'kalax1011/personal-website'
        // DOCKERHUB_CREDENTIALS_PSW = 'kodok1011'
        // DOCKERHUB_CREDENTIALS_USR = 'kalax1011'
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

        stage('Login to Docker Hub') {      	
            steps{                       	
                    //sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -username $DOCKERHUB_CREDENTIALS_USR --password-stdin' 
                    sh 'echo "kodok1011" | docker login -u kalax1011 --password-stdin'               		
                    echo 'Login Completed'      
            }           
        }   

        stage('Push Image to Docker Hub') {         
            steps{                            
                    sh 'docker push $DOCKER_IMAGE:$BUILD_NUMBER'           
                    echo 'Push Image Completed'       
            }            
        }  
}

    post {
        always {  
	        sh 'docker logout'     
        }   
        success {
            echo 'Pipeline succeeded! Docker image built and pushed.'
        }
        failure {
            echo 'Pipeline failed! Handle errors if needed.'
        }
    }
}