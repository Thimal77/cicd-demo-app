pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = 'thimal77'
        IMAGE_NAME = 'cicd-demo-app'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Pulling code from Gitea...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies...'
                sh '''
                    curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
                    apt-get install -y nodejs
                    cd app && npm install
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'cd app && npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t thimal77/${IMAGE_NAME}:build-${BUILD_NUMBER} ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing image to Docker Hub...'
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh "docker push thimal77/${IMAGE_NAME}:build-${BUILD_NUMBER}"
                }
            }
        }

    }

    post {
        success {
            echo 'Pipeline completed! Image pushed to Docker Hub.'
        }
        failure {
            echo 'Pipeline failed. Check the logs above.'
        }
    }
}