pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t my-react-app .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run my-app npm test'
            }
        }
        stage('Push') {
            steps {
                withCredentials([dockerRegistry]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD $DOCKER_REGISTRY_URL'
                    sh 'docker tag my-app $DOCKER_REGISTRY_URL/my-app'
                    sh 'docker push quikky/demo-app:my-app-1.0'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yml'
            }
        }
    }
}
