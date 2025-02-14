pipeline {
    agent {
        docker {
            image 'eclipse-temurin:23-jdk'  // Java 23 for builds
            args '--user root'
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
        stage('Install Maven'){
            steps{
                sh '''
                    apt-get update
                    apt-get install -y maven
                    mvn -version
                '''
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