pipeline {
    agent any
    tools {
        // maven 'maven3.9.9',
        jdk 'jdk-23'
    }
    stages {
        stage('Hello World') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Print JAVA_HOME'){
            steps {
                sh '''
                echo "JAVA_HOME: $JAVA_HOME"
                java -version
                '''
            }
        }
        stage('Build') {
            steps {
                echo 'Build stage...'
                sh 'mvn clean install -DskipTests'
            }
        }
    }
}