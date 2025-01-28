pipeline {
    agent any
    tools {
        maven 'maven3.8'
    }
    stages {
        stage('Hello World') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Build') {
            steps {
                echo 'Build stage...'
                mvn clean install -DskipTests
            }
        }
    }
}