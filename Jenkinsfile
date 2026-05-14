pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = 'Docker-credentials' 
        IMAGE_NAME = 'YOUR_USERNAME/new_docker_image' 
    }
    stages {
        stage('Build Java') { steps { bat 'javac HelloWorld.java' } }
        stage('Run Java') { steps { bat 'java HelloWorld' } }
        stage('Build Docker') { steps { bat 'docker build -t %IMAGE_NAME%:latest .' } }
        stage('Login DockerHub') {
            steps {
               withCredentials([usernamePassword(credentialsId: 'Docker-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'echo %PASS%| docker login -u %USER% --password-stdin'
                }
            }
        }
        stage('Push Image') { steps { bat 'docker push %IMAGE_NAME%:latest' } }
    }
}
