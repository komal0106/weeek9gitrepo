
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t weeek9image:v1 ."
            }
        }

        stage('Docker Login') {
            steps {
                echo "Logging in to Docker Hub"
                bat "docker login -u komal0106"
                   bat "docker login -u komal0106 -p guddu2006"
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                echo "Push Docker Image to Docker Hub"
                bat "docker tag weeek9image:v1 komal0106/weeek9image:latest"
                bat "docker push komal0106/weeek9image:latest"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying application to Kubernetes"
                bat "kubectl apply -f deployment.yaml --validate=false"
                bat "kubectl apply -f service.yaml"
            }
        }

        stage('Verify Kubernetes Deployment') {
            steps {
                echo "Checking Kubernetes resources"
                bat "kubectl get deployments"
                bat "kubectl get pods"
                bat "kubectl get services"
            }
        }
    }

    post {
        success {
            echo 'PIPELINE COMPLETED SUCCESSFULLY!'
            echo 'Docker Image: komal0106/weeek9image:latest'
            echo 'Kubernetes deployment completed successfully!'
        }

        failure {
            echo 'PIPELINE FAILED!'
            echo 'Please check the logs.'
        }
    }
}
