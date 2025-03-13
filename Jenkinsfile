pipeline {
    agent any
environment {
        DOCKER_IMAGE = 'dndot/adservice:latest'
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t $DOCKER_IMAGE ."
                    }
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push $DOCKER_IMAGE"
                    }
                }
            }
        }
    }
        stage('Deploy to Production') {
            steps {
                sh 'docker run -d -p 3000:3000 --name nextjs-app $DOCKER_IMAGE'
            }
        }
    }
}

