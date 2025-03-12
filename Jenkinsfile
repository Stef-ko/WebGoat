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
        //stage('Build and SonarQube Scan') {
        //    steps {
        //        withSonarQubeEnv(installationName: "SonarScanner") {
        //          sh "mvn sonar:sonar -Dsonar.projectKey=WebGoat_Jenkins -Dsonar.projectName='WebGoat_Jenkins'"
        //        }
        //    }
        //}
    }
}
