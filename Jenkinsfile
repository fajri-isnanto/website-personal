pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('kalax1011')
        DOCKER_IMAGE = 'kalax1011/personal-website'
        DOCKER_REPO = 'kalax1011/personal-website'
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
                    sh 'docker push $DOCKER_IMAGE'           
                    echo 'Push Image Completed'       
            }            
        }  

        stage('SSH to Docker Server') {
            steps{
                //ssh to server
                sh 'sshpass -p "!qwerty7" ssh root@172.20.103.221'
                sh 'docker pull $DOCKER_REPO'
            }
        }
        stage('Stop Docker Container') {
            steps{
                sh 'docker container stop ${DOCKER_IMAGE}'
                sh 'docker container rm ${DOCKER_IMAGE}'
            }
        }
        stage('Start Docker Container') {
            steps{
                sh 'docker run -d --name ${DOCKER_IMAGE} -p 8020:8030 ${DOCKER_IMAGE}'
            }
        }
        stage('cek container running') {
            steps{
                sh 'curl http://172.20.103.226:8030'
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