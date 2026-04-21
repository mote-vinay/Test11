pipeline {
    agent any

    environment {
        IMAGE_NAME = "registration-form"
        CONTAINER_NAME = "registration-container"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop $CONTAINER_NAME || true'
                sh 'docker rm $CONTAINER_NAME || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 80:80 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }

        stage('Publish HTML (optional)') {
            steps {
                publishHTML([
                    reportDir: '.',
                    reportFiles: 'index.html',
                    reportName: 'HTML Preview'
                ])
            }
        }
    }
}
