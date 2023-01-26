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
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=Jenkins-frontend -Dsonar.organization=brunosantos1388 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=599b56c3dd40d5744bef783dbdd4d4f8bdc87e0c'
			}
    }

}
}