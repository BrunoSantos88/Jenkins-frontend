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
  -Dsonar.login=sqp_637cf72af2019a94744d0d04dc43fee5b91eece5'
			}
    }
}
}