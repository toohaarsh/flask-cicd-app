pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-webapp:latest"
        CONTAINER_NAME = "flask-webapp-container"
        DOCKER_PATH = "C:\\Program Files\\Docker\\Docker\\Resources\\bin\\docker.exe"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                git 'https://github.com/toohaarsh/flask-cicd-app'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    bat "\"${DOCKER_PATH}\" build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                script {
                    bat "\"${DOCKER_PATH}\" run -d -p 5000:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                }
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Cleaning up old containers...'
                script {
                    bat "\"${DOCKER_PATH}\" container prune -f"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
