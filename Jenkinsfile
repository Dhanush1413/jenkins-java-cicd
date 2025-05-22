pipeline {
    agent any

    environment {
        IMAGE_NAME = 'dhanushvenkatachalam/demo-app:latest'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Dhanush1413/jenkins-java-cicd.git'
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                retry(3) {
                    bat "docker build -t %IMAGE_NAME% ."
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                        echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                        docker push %IMAGE_NAME%
                    """
                }
            }
        }
    }
}
