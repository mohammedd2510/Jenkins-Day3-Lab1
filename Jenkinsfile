pipeline {
    agent { label 'docker' } // Specify the agent label
    environment {
        DOCKER_IMAGE = 'mosama25/jenkins_day3_lab1:v4.0'
        DOCKER_LOGIN_CREDS = credentials('docker_credentials')// Replace with your Jenkins credentials ID
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from SCM
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'echo "<your_password>" | sudo -S chmod 666 /var/run/docker.sock'
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                echo 'Logging into Docker Hub...'
                sh '''
                    echo "$DOCKER_LOGIN_CREDS_PSW" | docker login -u mosama25 --password-stdin
                '''
            }
        }
        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image...'
                sh 'docker push $DOCKER_IMAGE'
            }
        }
    }
}
