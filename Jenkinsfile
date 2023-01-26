pipeline {
    agent any

    stages {
        stage('Example Build') {
            agent { docker 'maven:3.8.7-eclipse-temurin-11' } 
            steps {
                echo 'Hello, Maven'
                sh 'mvn --version'
            }
        }
    }
}