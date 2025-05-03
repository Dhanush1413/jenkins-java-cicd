pipeline {
    agent any

    tools {
        maven 'Maven 3.9.4' // Must match the Maven name in Global Tool Configuration
    }

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
                    def app = docker.build("${IMAGE_NAME}")
                    docker.withRegistry('', 'dockerhub-creds-id') {
                        app.push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                bat "docker run -d -p 8080:8080 ${IMAGE_NAME}"
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
