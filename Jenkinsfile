
pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')  // Check GitHub every 2 minutes
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/mote-vinay/Test11.git'
            }
        }

        stage('Build (Optional)') {
            steps {
                echo 'No Docker build - add your build steps here if needed'
            }
        }

        stage('Publish HTML') {
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
