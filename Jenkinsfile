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

    stage('Clone repository') { 
steps { 
script{
checkout scm
}
}
}

    stage('SonarCloud-GateCode-Quality') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=Jenkins-frontend -Dsonar.organization=brunosantos88 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=f8240d7caaf43a5abea893e3c0960b481f5ad3a6'
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