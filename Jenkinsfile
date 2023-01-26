pipeline {
    agent { docker { image 'node:6.3' } }
    stages {
        stage('Node Agent') {
            steps {
                sh 'npm install'
            }
        }

stage('GIT CLONE') {
  steps {
                // Get code from a GitHub repository
    git url: 'https://github.com/BrunoSantos88/Jenkins-frontend.git', branch: 'main',
    credentialsId: 'jenkins-aws'
          }
  }

stage ('Build docker image') { //here you can check how you can build even docker images inside container
        agent {
            docker {
                image 'maven:latest'
            }
        }
}

  stage('Synk-GateSonar-Security') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
  }

    }
}