
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "motevinay/user-registration1"
        DOCKER_CREDENTIALS = "docker-hub-creds"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/mote-vinay/Test11.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${BUILD_NUMBER} ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: "${DOCKER_CREDENTIALS}",
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )]) {
                        sh """
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        """
                    }
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    sh "docker push ${DOCKER_IMAGE}:${BUILD_NUMBER}"
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh """
                    docker stop myapp || true
                    docker rm myapp || true
                    docker run -d --name myapp -p 8080:80 ${DOCKER_IMAGE}:${BUILD_NUMBER}
                    """
                }
            }
        }
    }
}
