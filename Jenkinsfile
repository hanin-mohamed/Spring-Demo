pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/hanin-mohamed/Spring-Demo'
            }
        }
        stage('Build with Maven') {
            agent {
                docker {
                    image 'maven:3.8.5-openjdk-17'
                }
            }
            steps {
                sh 'mvn clean package'
            }
        }
    }
}