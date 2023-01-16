pipeline {
  agent any

  tools { 
        ///depentencias 
        maven 'Maven 3.6.3' 
        terraform 'Terraform 1.3.7' 
    }

// Stages.
  stages {   

    stage('Slack Notification(Start)') {
      steps {
        slackSend message: 'Pipeline Inciada!. Necessidade de atenção, caso seja em Produção!'

}
}


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

///DockerProcesso
stage('Docker Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                 script{
                 app =  docker.build("frontend")
               }
            }
    }
}

stage('Docker Push') {
            steps {
                script{
                    docker.withRegistry('https://555527584255.dkr.ecr.us-west-2.amazonaws.com','ecr:us-west-2:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
}
    	}
	    
  }
