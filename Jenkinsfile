pipeline {
    agent any
    
    
    stages {
        // Checkout SCM
        stage('Checkout SCM'){
            steps{
                sh 'echo "Cloning repo..."'
                git branch: 'main', url: 'https://github.com/Stef-ko/WebGoat'
            }
        }
        // SAST WITH SONARQUBE CLOUD
        stage('Build + SonarQube Cloud Scan'){
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
        // SCA WITH OWASP DEPENDENCY CHECK
        stage('Software Composition Analysis with OWASP Dependency Check'){
            steps {
                echo 'SCA...'
                dependencyCheck additionalArguments: '--prettyPrint', nvdCredentialsId: 'NVDAPIKEY', odcInstallation: 'SCA'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }
}
