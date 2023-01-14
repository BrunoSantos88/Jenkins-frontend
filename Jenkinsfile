pipeline {
  agent any
  tools { 
        maven 'Maven 3.5.2'  
    }

stages{


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

///DockerProcesso
stage('Socker Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin88", url: ""]) {
                 script{
                 app =  docker.build("frontend")
                 }
               }
            }
    }

stage('Docker Push') {
            steps {
                script{
                    docker.withRegistry('https://555527584255.dkr.ecr.us-west-2.amazonaws.com', 'ecr:us-west-2:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
    	}
}
}
