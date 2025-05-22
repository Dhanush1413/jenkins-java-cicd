pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-creds' // Replace with your Jenkins DockerHub credentials ID
        IMAGE_NAME = 'dhanushvenkatachalam/demo-app:latest'             // Your DockerHub repo
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Dhanush1413/jenkins-java-cicd.git
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "$DOCKER_CREDENTIALS_ID", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }
    }
}
