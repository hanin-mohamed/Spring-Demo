pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'demo-spring-app'
        CONTAINER_NAME = 'spring-container'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/hanin-mohamed/Spring-Demo'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        stage('Run Docker Container') {
            steps {
                sh "docker stop ${CONTAINER_NAME} || true && docker rm ${CONTAINER_NAME} || true && docker run -d -p 8082:8081 --name ${CONTAINER_NAME} ${DOCKER_IMAGE}"
            }
        }
    }
}