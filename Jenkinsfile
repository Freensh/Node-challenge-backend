pipeline {
    agent any

    environment {
        registry = '939083599624.dkr.ecr.us-east-1.amazonaws.com/node_backend'
        registryCredential = 'challenge'
        dockerImage = ''
    }
    stages {
        stage ('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/Freensh/Node-challenge-backend.git'
            }
        }

        stage ('Install dependencies'){
            steps {
                sh 'npm install'
            }
        }

        stage ('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage ('Build docker container') {
            steps{
                script {
                    dockerImage = docker.build "challenge-backend:$BUILD_NUMBER"
                }
            }
        }
        stage('Push Image to ECR') {
            steps {
                script {
                    docker.withRegistry("https://"+registry, "ecr:us-east-1:"+registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deployment'){
            steps {

            }
        }
    }
}