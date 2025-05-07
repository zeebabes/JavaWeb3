pipeline {
    agent any
 
    environment {
        DOCKER_HUB_CREDENTIALS = 'Docker-Hub-Credentials'
        IMAGE_NAME = 'kemiagbabiaka/java-web-calculator'
    }
 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'latest', url: 'https://github.com/zeebabes/JavaWeb3.git'
            }
        }
 
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }
 
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_HUB_CREDENTIALS}") {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }
}
