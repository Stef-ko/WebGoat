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
        stage('SonarQube Analysis') {
            // def mvn = tool 'mvn';
            steps {
                sh 'echo "Running SonarQube..."'
                sh 'mvn exec:java -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args="install-deps"'
                withSonarQubeEnv(credentialsId: 'SonarQube_Token', installationName: 'SonarQube_Server') {
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=WebGoatMA -Dsonar.projectName='WebGoatMA'"
                }
            }
        }
        stage("Quality Gate"){
            timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
                def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
                if (qg.status != 'OK') {
                    error "Pipeline aborted due to quality gate failure: ${qg.status}"
                }
            }
        }
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