pipeline {
    agent any

    environment {
        IMAGE_NAME = 'kemiagbabiaka/java-web-calculator'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/zeebabes/JavaWeb3.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                        echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }
    }
}
