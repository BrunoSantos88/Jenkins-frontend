pipeline {
  agent any
  
  tools { 
        ///depentencias 
        maven 'Maven 3.6.3' 
    }

stages {   

stage('Clone repository') { 
steps { 
script{
checkout scm
}
}
}
 
stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=DveloperFrontend \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login='
			}
    }
}
}