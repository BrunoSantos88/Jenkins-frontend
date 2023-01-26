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


stage ('Maven') {
   agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
}
    }
}
