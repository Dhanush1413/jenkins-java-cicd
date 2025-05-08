pipeline {
    agent any

    environment {
        IMAGE_NAME = 'dhanushv167/demo-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dhanush1413/jenkins-java-cicd.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    def app = docker.build("${IMAGE_NAME}:latest")
                    docker.withRegistry('', 'dockerhub-creds-id') {
                        app.push("latest")
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker rm -f demo-app || exit 0'
                bat "docker run -d -p 8080:8080 --name demo-app ${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment successful!'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
