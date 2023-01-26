pipeline {
    agent { docker { image 'maven:3.8.7-eclipse-temurin-11' } }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }

 stage('Checkout code') {
        steps {
            checkout scm
        }
    }


    stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=Jenkins-frontend -Dsonar.organization=brunosantos881388 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=58de857afff27d95c16d759d1134e1f912bd51fb'
			}
    }

    
    }
}