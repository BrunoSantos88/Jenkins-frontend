pipeline {
    agent none
    stages {
        stage('Back-end') {
            agent {
                docker { image 'maven:3.8.7-eclipse-temurin-11' }
            }
            steps {
                sh 'mvn --version'
            }
        }

  
    }
}