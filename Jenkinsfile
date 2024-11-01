pipeline {
    agent any
    environment {
        DOCKER_REGISTRY = "mohitsharma552"
        IMAGE_NAME = "Minikube-Jenkins-Docker"
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Build Docker image
                    sh '''#!/bin/bash
                    docker build -t $DOCKER_REGISTRY/$IMAGE_NAME:${BUILD_ID} .
                    '''
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    // Push Docker image to registry
                    sh '''#!/bin/bash
                    docker push $DOCKER_REGISTRY/$IMAGE_NAME:${BUILD_ID}
                    '''
                }
            }
        }
        stage('Deploy to Minikube') {
            steps {
                script {
                    // Apply Kubernetes manifests
                    sh 'kubectl apply -f kubernetes/deployment.yaml'
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
