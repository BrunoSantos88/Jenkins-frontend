pipeline {

    agent {
        docker {
            image 'node'
            args '-u root'
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }


  stage('GIT CLONE') {
  steps {
                // Get code from a GitHub repository
    git url: 'https://github.com/BrunoSantos88/Jenkins-frontend.git', branch: 'main',
    credentialsId: 'jenkins-aws'
          }
  }
    
  stage('SonarAnalysis') {
        steps {	
        sh "npm install"
		sh 'sonar:sonar \
  -Dsonar.projectKey=DeveloperFrontend \
  -Dsonar.host.url=http://3.238.149.127:9000 \
  -Dsonar.login=sqp_6d2b3325ebdeb23c964211b9629b6f9f1c6a8f66'
			}
    }

    }
}


  
