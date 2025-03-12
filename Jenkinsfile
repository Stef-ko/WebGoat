pipeline {
    agent any
    
    
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
        // WORKING SAST WITH SONARQUBE CLOUD
        stage('Build and SonarQube Cloud Scan'){
            agent {
                docker { 
                    image 'maven:3.9.9-eclipse-temurin-23'
                    args "--mount type=bind,source=${env.WORKSPACE},target=/workspace"
                }
            }
            steps {
                echo 'SAST...'
                sh 'cd /workspace && mvn org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=stef-ko_webgoat'
            }
        }
        // WORKING SCA WITH OWASP DEPENDENCY CHECK
        stage('Software Composition Analysis'){
            steps {
                echo 'SCA...'
                dependencyCheck additionalArguments: '--prettyPrint', nvdCredentialsId: 'NVDAPIKEY', odcInstallation: 'SCA'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }
}
