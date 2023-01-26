pipeline {
  agent any
  stages {
    stage('SonarQube analysis') {
      tools {
        sonarQube 'SonarQube Scanner 2.8'
      }
      steps {
        withSonarQubeEnv('SonarQube Scanner') {
          sh 'sonar-scanner'
        }
      }
    }
  }
}