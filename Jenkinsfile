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
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'dhanushvenkatachalam', passwordVariable: 'dckr_pat_mS2FwVLMRtdI-t4irNPs5XjRmzk')]) {
                    bat "docker login -u %DOCKER_USER% -p %DOCKER_PASS%"
                    bat "docker push %IMAGE_NAME%"
                }
            }
        }
    }
}
