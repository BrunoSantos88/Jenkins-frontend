pipeline {
  agent any
  tools { 
        maven 'Maven 3.6.3'  
    }

    environment {
    registry = "brunosantos88/awsfrontend"
    registryCredential = 'dockerlogin'
    dockerImage = ''
  }


  stages{

    stage('SonarCloud-GateCode-Quality') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=Jenkins-frontend -Dsonar.organization=brunosantos88-1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=c53123a613038f737e70be1e44643de7460ce9d8'
			}
        } 
    stage('Synk-GateSonar-Security') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
  }
  
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
   }
}