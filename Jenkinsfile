pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerlogin')
  }

  tools { 
        ///depentencias 
        maven 'Maven 3.6.3' 
    }

stages {   

stage('GIT CLONE') {
  steps {
                // Get code from a GitHub repository
    git url: 'https://github.com/BrunoSantos88/Jenkins-frontend.git', branch: 'main',
    credentialsId: 'jenkins-aws'
          }
  }

stage('SonarQube Analysis') {
    withSonarQubeEnv() {
      sh "${mvn}/usr/share/maven clean verify sonar:sonar -Dsonar.projectKey=DeveloperFrontend"
    }
  }

stage('Synk-GateSonar-Security') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
  }

///DockerProcesso
   stage('Docker Build') {
      steps {
        sh 'docker build -t brunosantos88/awsfrontend frontend/.'
     }
    }

   stage('Docker Login') {
      steps {
       sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
     }
    }
   
   stage('Docker Push') {
     steps {
        sh 'docker push brunosantos88/awsfrontend:latest'
     }
   }


   stage('Kubernetes Frontend') {
	   steps {
	      withKubeConfig([credentialsId: 'kubelogin']) {
		  sh ('kubectl apply -f frontend.yaml --namespace=developer')
		}
	      }
   	}

   stage ('AGUARDAR 180s INSTALAÇÂO OWSZAP'){
	  steps {
		  sh 'pwd; sleep 180; echo "Application Has been deployed on K8S"'
	 	}
	  }
	   
stage('OWSZAP PROXI FRONTEND') {
    steps {
		withKubeConfig([credentialsId: 'kubelogin']) {
		sh('zap.sh -cmd -quickurl http://$(kubectl get services/frontend --namespace=developer-o json| jq -r ".status.loadBalancer.ingress[] | .hostname") -quickprogress -quickout ${WORKSPACE}/zap_report.html')
	  archiveArtifacts artifacts: 'zap_report.html'
	}
	  }
    } 

}
}
  
