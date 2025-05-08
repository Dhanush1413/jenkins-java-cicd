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
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    def image = docker.build("${IMAGE_NAME}")
                    docker.withRegistry('', 'dockerhub-creds-id') {
                        image.push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Stop and remove any existing container using the same name
                    sh '''
                        docker rm -f demo-app-container || true
                        docker run -d --name demo-app-container -p 8080:8080 ${IMAGE_NAME}
                    '''
                }
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
