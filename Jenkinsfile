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
                bat 'docker build -t jenkins-web-app .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker rm -f jenkins-web-app-container 2>NUL'
                bat 'docker run -d --name jenkins-web-app-container -p 8081:80 jenkins-web-app'
            }
        }
    }
}
