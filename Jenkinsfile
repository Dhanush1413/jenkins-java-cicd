pipeline {
    agent any

    environment {
        IMAGE_NAME = 'yourdockerhubusername/yourimage:latest'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Dhanush1413/jenkins-java-cicd.git'
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat "docker login -u %DOCKER_USER% -p %DOCKER_PASS%"
                    bat "docker push %IMAGE_NAME%"
                }
            }
        }
    }
}
