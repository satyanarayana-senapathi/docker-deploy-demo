pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials("docker_id")
        IMAGE_NAME = "my-react-app"
        IMAGE_TAG = "latest"
        DOCKERHUB_REPO = "quikky/demo-app"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t $DOCKERHUB_REPO:$IMAGE_TAG .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run $DOCKERHUB_REPO:$IMAGE_TAG npm test'
            }
        }
        stage('Push') {
            steps {
                withCredentials([DOCKERHUB_CREDENTIALS]) {
                    sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                    sh "docker push $DOCKERHUB_REPO:$IMAGE_TAG"
                }
            }
        }
    }
}

