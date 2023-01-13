pipeline {
  agent any

  tools { 
        ///depentencias 
        maven 'Maven 3.5.2' 
    }

// Stages.
  stages {   

    stage('Slack Notification(Start)') {
      steps {
        slackSend message: 'Pipeline Inciada!. Necessidade de atenção, caso seja em Produção!'

}
}

    stage('Clone repository') { 
      steps { 
        script{
          checkout scm
            }
             } 
    }

  stage('Slack Notification(test unit code and vulnerability)') {
    steps {
      slackSend message: 'Pipeline está no estagio de teste no codigo. O Processo será realiazado no Quality Gate, são teste de Sonar e Synk, ambos vão verificar "bugs e vulnerabilidade" em nosso codigo!'

}
}
 
   ///Qualite gate
    stage('SonarCloud-GateCode-Quality') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=Jenkins-frontend -Dsonar.organization=brunosantos881388 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=7b32cd52dd86a05d7d4d360fc414c8acb2ac14de'
			}
        } 
    stage('Synk-GateSonar-Security') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
  }

  stage('Slack Notification(Dockerization)') {
    steps {
      slackSend message: 'Arquivos estão compactados no docker!'

}
}

  stage('Docker Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                 script{
                 app =  docker.build("frontend")
                 }
               }
            }
    }

	stage('Dockr Push ECR') {
            steps {
                script{
                    docker.withRegistry('555527584255.dkr.ecr.us-east-1.amazonaws.com', 'ecr.us-east-1:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
    	}
	    
  }

   
// Email Notification
      post {
        always {
            echo "Notifying build result by email"
        }
        success {
            mail to: 'infratidevops@gmail.com',
                 subject: "SUCCESS: ${currentBuild.fullDisplayName}",
                 body: "Pipeline passou, Efetou com Sucesso"

        }
        failure {
           mail to: 'infratidevops@gmail.com',
                subject:"FAILURE: ${currentBuild.fullDisplayName}",
                body: "Pipeline Falhou , verificar os parametros corretos!"

        }
      }
}



   
