// pipeline {
//     agent any
//     environment {
//         DOCKERHUB_CREDENTIALS=credentials("docker_id")
//     }
//     stages {
//         stage('Checkout') {
//             steps {
//                 checkout scm
//             }
//         }
//         stage('Build') {
//             steps {
//                 sh 'docker build -t my-react-app .'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh 'docker run my-app npm test'
//             }
//         }
//         stage('Push') {
//             steps {
//                 withCredentials([dockerRegistry]) {
//                     sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD $DOCKER_REGISTRY_URL'
//                     sh 'docker tag my-app $DOCKER_REGISTRY_URL/my-app'
//                     sh 'docker push quikky/demo-app:my-app-1.0'
//                 }
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 sh 'kubectl apply -f deployment.yml'
//             }
//         }
//     }
// }




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
        stage('Login'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh "docker push $DOCKERHUB_REPO:$IMAGE_TAG"
                }
        }
    }
}

