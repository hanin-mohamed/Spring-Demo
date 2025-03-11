pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'demo-spring-app'
        CONTAINER_NAME = 'spring-container'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/hanin-mohamed/Spring-Demo'
            }
        }
        stage('Build with Maven') {
            steps {
                script {
                    docker.image('maven:3.8.5-openjdk-17').inside('-v /root/.m2:/root/.m2') {
                        sh 'mvn clean install'
                    }
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                docker run --rm -d -p 8082:8081 --name $CONTAINER_NAME $DOCKER_IMAGE
                '''
            }
        }
    }
}