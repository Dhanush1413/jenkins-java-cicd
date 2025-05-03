pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dhanushvenkatachalam/demo-app'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Docker Login and Push') {
            steps {
                script {
                    // Login to Docker registry with the correct credentials
                    withDockerRegistry([ credentialsId: 'dockerhub-creds', url: 'https://index.docker.io/v1/' ]) {
                        // Push the Docker image to Docker Hub
                        sh 'docker push $DOCKER_IMAGE'
                    }
                }
            }
        }
    }
}
