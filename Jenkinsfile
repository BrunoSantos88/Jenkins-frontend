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

  stage('SonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=DeveloperFrontend \
  -Dsonar.host.url=http://54.224.29.178:9000 \
  -Dsonar.login=sqp_81bece67cc962f88f1650bfccfe775b3c79362b2'
			}
    }
  
    }
}

  