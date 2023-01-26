pipeline {
  agent none
  stages {
    stage('snyk dependency scan') {
      agent {
        docker {
          image 'snyk/snyk:maven-3-jdk-11'
        }
      }
      environment {
        SNYK_TOKEN = credentials('SNYK_TOKEN')
      }	
      steps {
        sh 'mvn snyk:test -fn'
      }
    }
  }
}


  