pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker image'
                bat 'docker build -t jenkins-web-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Checking Docker image'
                bat 'docker image inspect jenkins-web-app'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying web application using Docker'

                bat '''
                    docker rm -f jenkins-web-app-container 2>NUL
                    if errorlevel 1 exit /b 1
                '''

                bat 'docker run -d --name jenkins-web-app-container -p 8081:80 jenkins-web-app'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
            echo 'Open http://localhost:8081'
        }

        failure {
            echo 'Pipeline failed. Check the Console Output.'
        }
    }
}
