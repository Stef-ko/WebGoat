pipeline {
    agent any

    tools {
        // maven 'mvn'
        jdk 'jdk23'
    }
    // {
    //     // docker {
    //     //     image 'eclipse-temurin:23-jdk'  // Java 23 for builds
    //     //     args '--user root'
    //     // }
    // }
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
        stage('Print JAVA_HOME'){
            steps {
                sh '''
                echo "JAVA_HOME: $JAVA_HOME"
                java -version
                '''
            }
        }
        stage('Build with Docker and SonarQube') {
            agent {
                docker {
                    image 'maven:3.9.9-amazoncorretto-23'
                }
            }
            steps {
                script {
                    sh 'java -version'  // Verify Java 23 is installed
                    echo "JAVA_HOME: $JAVA_HOME"
                    // sh 'mvn -version'   // Verify Maven version
                    sh "${mvn}/bin/mvn clean compile"
                    sh "${mvn}/bin/mvn compile sonar:sonar -Dsonar.projectKey=WebGoatMA -Dsonar.projectName='WebGoatMA'"
                }
            }
        }
        // stage('Building incl. SonarQube') {
        //     steps {
        //         script {
        //             sh 'echo "Running SonarQube..."'
        //             def mvn = tool 'maven';
        //             withSonarQubeEnv(credentialsId: 'Sonar_Token', installationName: 'SonarQube_Server') {
        //                 sh "${mvn}/bin/mvn compile sonar:sonar -Dsonar.projectKey=WebGoatMA -Dsonar.projectName='WebGoatMA'"
        //             }
        //         }
        //     }
        // }

        // stage('Build and Test'){
        //     steps{
        //         sh "mvn clean compile"
        //     }
        // }


        // stage('Install Maven'){
        //     steps{
        //         sh '''
        //             apt-get update
        //             apt-get install -y maven
        //             mvn -version
        //         '''
        //     }
        // }
        
        // stage('SonarQube Analysis') {
        //     // def mvn = tool 'mvn';
        //     steps {
        //         sh 'echo "Running SonarQube..."'
        //         sh 'mvn exec:java -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args="install-deps"'
        //         withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'SonarQube_Server') {
        //             sh "mvn clean verify sonar:sonar -Dsonar.projectKey=WebGoatMA -Dsonar.projectName='WebGoatMA'"
        //         }
        //     }
        // }
        // stage("Quality Gate"){
        //     steps{
        //         ttimeout(time: 1, unit: 'HOURS') {
        //             // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
        //             // true = set pipeline to UNSTABLE, false = don't
        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }
        // stage('SonarQube Analysis') {
        //     steps{
        //         // def mvn = tool 'Default Maven';
        //         sh 'echo "Running SonarQube..."'
        //         withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'lil sonar installation') {
        //             sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=WebGoat_MA -Dsonar.projectName='WebGoat_MA'"
        //         }
        //     }
        // }
        // stage('Run SonarQube'){
        //     environment {
        //         scannerHome = tool 'lil-sonar-tool';
        //     }
        //     steps {
        //         sh 'echo "Running SonarQube..."'
        //         withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'lil sonar installation') {
        //             sh "${scannerHome}/bin/sonar-scanner"
        //         }
        //     }
        // }
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