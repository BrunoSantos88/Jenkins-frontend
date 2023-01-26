pipeline {
    agent { docker { image 'node:6.3' } }

    stages {

stage('GIT CLONE') {
  steps {
                // Get code from a GitHub repository
    git url: 'https://github.com/BrunoSantos88/Jenkins-frontend.git', branch: 'main',
    credentialsId: 'jenkins-aws'
          }
  }

  stages {
    stage('snyk dependency scan') {
      tools {
        snyk 'snyk-latest'
      }	
      steps {
        snykSecurity(
          organisation: 'Jenkins-frontend',
          severity: 'high',
          snykInstallation: 'snyk-latest',
          snykTokenId: 'snyk',
          failOnIssues: 'true'
        )		
      }
    }
}
}
}


  