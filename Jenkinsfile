pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/hanin-mohamed/Spring-Demo'
            }
        }
        stage('Build with Maven') {
            steps {
                sh '''
                docker run --rm -v $(pwd):/app -w /app maven:3.8.5-openjdk-17 mvn clean package
                '''
            }
        }
        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t demo-spring-app .
                '''
            }
        }
        stage('Run Docker Container') {
            steps {
                sh '''
                docker stop spring-container || true
                docker rm spring-container || true
                docker run -d -p 8081:8081 --name spring-container demo-spring-app
                '''
            }
        }
    }
}