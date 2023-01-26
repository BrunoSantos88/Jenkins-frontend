pipeline {
  agent any
  

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerlogin')
  }

  tools { 
        ///depentencias 
        maven 'Maven 3.8.7' 
    }

stages {   

stage('GIT CLONE') {
  steps {
                // Get code from a GitHub repository
    git url: 'https://github.com/BrunoSantos88/Jenkins-frontend.git', branch: 'main',
    credentialsId: 'jenkins-aws'
          }
  }
 
stage('Synk-GateSonar-Security') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
  }

}

}