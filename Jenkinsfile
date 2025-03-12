pipeline {
    //agent any
    agent {
        docker { image 'maven:3.9.9-eclipse-temurin-23' }
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Checkout SCM'){
            steps{
                sh 'echo "Cloning repo..."'
                git branch: 'main', url: 'https://github.com/Stef-ko/WebGoat'
            }
        }
        stage('Build and SonarQube Cloud Scan'){
            steps {
                sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=stef-ko_webgoat'
            }
        }
        stage('Software Composition Analysis'){
            steps {
                sh 'echo "SCA..."'
                // Invoke OWASP Dependency-Check
                // Ensure that OWASP Dependency-Check is available in the system PATH
                dependencyCheck additionalArguments: '--prettyPrint', nvdCredentialsId: 'NVDAPIKEY', odcInstallation: 'SCA'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }
}
