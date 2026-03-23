pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'rizovamagdalena/nginx-test:latest'
        DOCKER_CREDENTIALS = 'b8af349b-065b-4be6-89b8-e14b63b39b55'     }
    stages {
        stage('Clone repository') {
            steps {
                git url: 'https://github.com/rizovamagdalena/simple-docker-nginx.git', branch: 'main'
            }
        }

        stage('Build Docker image') {
            steps {
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }

        stage('Push Docker image') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS}", passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    bat """
                    echo Logging into Docker Hub...
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                    docker push %DOCKER_IMAGE%
                    docker logout
                    """
                }
            }
        }
    }
}