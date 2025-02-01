pipeline {
    agent any
    tools {
        maven 'maven3.9.9'
        jdk 'jdk23'
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
        stage('Print Maven Version'){
            steps {
                sh '''
                echo "Maven Version"
                maven -version
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