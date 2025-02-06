pipeline {
    agent any
    // tools {
    //     // maven 'maven3.9.9'
    //     // jdk 'jdk23'
    // }
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
                sh 'mvn -version'
                '''
            }
        }
        stage('Clone repo'){
            steps{
                checkout scm: scmGit(branches: [[name: '*/main']], extensions: [], user)
            }
        }
        stage('Build') {
            steps {
                echo 'Build stage...'
                sh 'mvn -B -DskipTests clean package'
                // sh 'mvn clean install -DskipTests'
            }
        }
    }
}