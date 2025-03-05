pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/nextjs-app:latest'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'staging', url: 'git@github.com:dndot/nextjs-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'docker run -d -p 3000:3000 --name nextjs-app $DOCKER_IMAGE'
            }
        }
    }
}

