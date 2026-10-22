pipeline {
    agent any

    stages {

       

        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t week9image:latest ."
            }
        }
        stage('Docker Login') {
            steps {
                  bat 'docker login -u komal0106 -p guddu2006'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag week9image:latest komal0106/week9repo:latest"

                bat "docker push komal0106/week9repo:latest"

            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                    // apply deployment & service
                    bat 'kubectl apply -f deployment.yaml --validate=false'
                    bat 'kubectl apply -f service.yaml'
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
