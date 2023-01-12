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

				sh 'mvn sonar:sonar -Dsonar.projectKey=Jenkins-frontend -Dsonar.host.url=http://141.148.3.32:9000 -Dsonar.login=hgcloGyvmzcIYIT6aC3i1HW6Q1HKvFERIzf6rr0bN74='

			}

		}

  stage('Email Sucess')
		{

			emailext (
				to: 'brunosantosc1@gmail.com',
				subject: "Sucess Pipeline: ${currentBuild.fullDisplayName}",
				body: "Sucess with ${env.BUILD_URL}"
				)	 
		}



	}catch (e) {

		stage('Email Failed')
		{

			emailext (
				to: 'brunosantosc1@gmail.com',
				subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
				body: "Something is wrong with ${env.BUILD_URL}"
				)	 
		}


		throw e
	}

	
}




   
