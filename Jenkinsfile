pipeline {

    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Build JAR') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Configure Minikube Docker') {
            steps {
                bat 'minikube -p minikube docker-env --shell cmd > docker-env.bat'
                bat 'call docker-env.bat'
                bat 'docker info'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t springboot-app:latest .'
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/deployment.yaml'
                bat 'kubectl apply -f k8s/service.yaml'
                bat 'kubectl rollout restart deployment springboot-app'
            }
        }

    }
}