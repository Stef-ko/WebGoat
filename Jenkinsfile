pipeline {
    agent {
        docker {
            image 'eclipse-temurin:23-jdk-jammy'  // Java 23 for builds
        }
    }
    stages {
        stage('Hello World'){
            steps {
                sh 'echo "Hello World"'
            }
        }
        stage('Build') {
            steps {
                sh 'echo "Build stage...'
                sh 'java -version'  // Confirm Java 23 is used
                sh 'mvn clean package -DskipTests'
            }
        }
    }
}