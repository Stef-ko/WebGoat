pipeline {
    agent any
    tools {
        maven 'maven3.9.9'
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