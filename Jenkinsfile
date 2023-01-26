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

  stage('CompileandRunSonarAnalysis') {
    steps {	
		sh 'sonar-scanner \
  -Dsonar.projectKey=DeveloperFrontend \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://54.224.29.178:9000 \
  -Dsonar.login=sqp_81bece67cc962f88f1650bfccfe775b3c79362b2'
			}
    }

stage('snyk dependency scan') {
      agent {
        docker {
          image 'snyk/snyk:maven-3-jdk-11'
        }
      }
      environment {
        SNYK_TOKEN = credentials('SNYK_TOKEN')
      }	
      steps {
        sh 'mvn snyk:test -fn'
      }
    }
    }
}


  