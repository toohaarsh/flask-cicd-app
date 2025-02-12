pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-webapp"
        CONTAINER_NAME = "flask-webapp-container"
        DOCKER_HUB_REPO = "harrsh24/flask-webapp"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'main', url: 'https://github.com/toohaarsh/flask-cicd-app'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                script {
                    sh 'docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME'
                }
            }
        }

        stage('Cleanup') {
            steps {
                echo 'Cleaning up old containers...'
                script {
                    sh '''
                        docker stop $CONTAINER_NAME || true
                        docker rm $CONTAINER_NAME || true
                        docker rmi $IMAGE_NAME || true
                    '''
                }
            }
        }
    }
}
