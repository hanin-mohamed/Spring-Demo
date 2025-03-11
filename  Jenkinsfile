pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'git@github.com:hanin-mohamed/Spring-Demo.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh './mvnw clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t demo-spring-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8081:8081 --name spring-container demo-spring-app'
            }
        }
    }
}
