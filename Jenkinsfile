pipeline {
  agent {
    dockerfile {
      customWorkspace '/test'
      filename 'Dockerfile'
    }
  }
  stages {
    stage('Compile static assets') {
      steps {
        sh 'node --version'
        sh 'npm --version'
        sh 'pwd'
        sh 'ls'
        sh 'npm run build'
      }
    }
  }
}
