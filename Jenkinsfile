// devps projects
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dhanushvenkatachalam/demo-app'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    bat 'docker build -t %DOCKER_IMAGE% .'
                }
            }
        }

        stage('Docker Login and Push') {
            steps {
                script {
                    withDockerRegistry([ credentialsId: 'dockerhub-creds', url: 'https://index.docker.io/v1/' ]) {
                        bat 'docker push %DOCKER_IMAGE%'
                    }
                }
            }
        }

        stage('Check Container Status') {
            steps {
                bat 'docker ps'
            }
        }
    }
}
