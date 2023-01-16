pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerlogin')
  }
  }


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
stages {
    stage('Build') {
      steps {
        sh 'docker build -t brunosantos88/awsfrontend .'
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
   
    stage('Push') {
      steps {
        sh 'docker push brunosantos88/awsfrontend'
      }
    }
  }
  }

