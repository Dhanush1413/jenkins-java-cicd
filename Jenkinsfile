pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dhanushvenkatachalam/demo-app'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Use Windows batch command instead of sh
                    bat 'docker build -t %DOCKER_IMAGE% .'
                }
            }
        }

        stage('Docker Login and Push') {
            steps {
                script {
                    // Use Windows batch command for Docker login and push
                    withDockerRegistry([ credentialsId: 'dockerhub-creds', url: 'https://index.docker.io/v1/' ]) {
                        bat 'docker push %DOCKER_IMAGE%'
                    }
                }
            }
        }
    }
}
