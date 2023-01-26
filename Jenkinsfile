pipeline {
    agent { docker { image 'maven:3.8.7-eclipse-temurin-11' } }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }
    
    stage('SonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=DeveloperFrontend \
  -Dsonar.host.url=http://3.238.149.127:9000 \
  -Dsonar.login=sqp_6d2b3325ebdeb23c964211b9629b6f9f1c6a8f66'
			}
    }

    }
}


  
