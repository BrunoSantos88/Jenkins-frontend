pipeline {
  agent any
  tools { 
        maven 'Maven 3.6.3'  
    }

  stages{

    stage('Clone repository') { 
steps { 
script{
checkout scm
}
}
}

stage('SonarQube analysis') {

			withSonarQubeEnv('sonarqube') {

				sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=-TechDay--Jenkins-Servidor-CI-CD -Dsonar.organization=brunosantos881388 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=ef814cbc7a3bebcd87e212e7638a2bd75e41bb62'

			}

		}
	}

	
}




   
