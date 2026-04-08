pipeline {
    agent any
    
    environment {
        REGISTRY = "your-registry.azurecr.io"
        IMAGE_NAME = "calculator-api"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code from GitHub..."
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo "Building Calculator API with Maven..."
                sh 'mvn clean package -DskipTests'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t ${REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} .'
                sh 'docker tag ${REGISTRY}/${IMAGE_NAME}:${IMAGE_TAG} ${REGISTRY}/${IMAGE_NAME}:latest'
            }
        }
    }
    
    post {
        always {
            echo "Build completed"
        }
    }
}