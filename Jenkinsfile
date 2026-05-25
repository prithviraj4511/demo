pipeline {

    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven'
    }

    environment {
        IMAGE_NAME = "springboot-app"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/prithviraj4511/jenk.git'
            }
        }

        stage('Build JAR') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Configure Minikube Docker') {
            steps {
                bat 'minikube -p minikube docker-env --shell powershell > minikube_env.ps1'
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
            }
        }

    }
}