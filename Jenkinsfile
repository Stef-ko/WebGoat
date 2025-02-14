pipeline {
    agent {
        docker {
            image 'maven:3.9.5-eclipse-temurin:23-jdk-alpine'  // Java 23 for builds
        }
    }
    stages {
        stage('Hello World'){
            steps {
                sh 'echo "Hello World"'
            }
        }
        stage('Clone repo'){
            steps{
                sh 'echo "Cloning repo..."'
                git branch: 'main', url: 'https://github.com/Stef-ko/WebGoat'
            }
        }
        stage('Build') {
            steps {
                sh 'echo "Build stage..."'
                sh 'java -version'  // Confirm Java 23 is used
                sh 'mvn --version'  // Confirm Maven is installed
                sh 'mvn clean package -DskipTests'
            }
        }
    }
}