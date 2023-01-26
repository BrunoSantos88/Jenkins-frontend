pipeline {
    agent { docker { image 'node:16.17.1-alpine' } }
    stages {
        stage('build') {
            steps {
                sh 'node --version'
            }
        }

    stage('GIT CLONE') {
  steps {
                // Get code from a GitHub repository
    git url: 'https://github.com/BrunoSantos88/Jenkins-frontend.git', branch: 'main',
    credentialsId: 'jenkins-aws'
          }
  }

    }
}


  
