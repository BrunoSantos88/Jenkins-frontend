pipeline {
  agent any
  

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerlogin')
  }

  tools { 
        ///depentencias 
        maven 'Maven 3.6.3' 
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


stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=DveloperFrontend \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=sqp_6f5da24a804dcd6e51601e83ee3993fc8d67a3ea'
                }
            }
        }

}

}