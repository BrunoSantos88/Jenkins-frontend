pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerlogin')
    SNYK_TOKEN = credentials('SNYK_TOKEN')
  }

  tools { 
        ///depentencias 
        maven 'Maven 3.6.3' 
    }
    
// Stages.
  stages {  
stage('GIT CLONE') {
  steps {
                // Get code from a GitHub repository
    git url: 'https://github.com/BrunoSantos88/Jenkins-frontend.git', branch: 'main',
    credentialsId: 'jenkins-aws'
          }
  }

stage('snyk dependency scan') {
      steps {
        sh 'mvn snyk:test -fn'
      }
    }
stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=brunosantos881388 -Dsonar.organization=jenkins-frontend -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=988c643e8219cd60fdebf4e8fbf30e4326edeb81'
			}
    }
  
    }
}