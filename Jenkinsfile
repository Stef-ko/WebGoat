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
        stage('Run SonarQube'){
            environment {
                scannerHome = tool 'lil-sonar-tool';
            }
            steps {
                sh 'echo "Running SonarQube..."'
                stage('SonarQube Analysis') {
                    def mvn = tool 'Default Maven';
                    withSonarQubeEnv() {
                        sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=WebGoat_MA -Dsonar.projectName='WebGoat_MA'"
                    }
                }
            }
        }
        // stage('Build') {
        //     steps {
        //         sh 'echo "Build stage..."'
        //         sh 'java -version'  // Confirm Java 23 is used
        //         sh 'mvn --version'  // Confirm Maven is installed
        //         sh 'mvn clean package -DskipTests'
        //     }
        // }
    }
}