pipeline {
    agent { docker { image 'maven:3.8.7-eclipse-temurin-11' } }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerlogin')
  }

    tools { 
        ///depentencias 
        maven 'Maven 3.8.7' 

    }

 stage('Checkout code') {
        steps {
            checkout scm
        }
    }
 
stage('Synk-GateSonar-Security') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
}

///Docker STEPS
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
  
  stage('Kubernetes Deployment frontend') {
	   steps {
	    withKubeConfig([credentialsId: 'kubelogin']) {
		  sh ('kubectl apply -f frontend.yaml --namespace=developer')
		}
	     }
   	}

    stage ('AGUARDAR 180s INSTALAÇAO OWSZAP'){
	  steps {
    sh 'pwd; sleep 180; echo "Application Has been deployed on K8S"'
	  	}
	   }
	   

stage('OWSZAP PROXI frontend') {
    steps {
		withKubeConfig([credentialsId: 'kubelogin']) {
		sh('zap.sh -cmd -quickurl http://$(kubectl get services/frontend --namespace=developer -o json| jq -r ".status.loadBalancer.ingress[] | .hostname") -quickprogress -quickout ${WORKSPACE}/zap_report.html')
	  archiveArtifacts artifacts: 'zap_report.html'
	}
	  }
      
    } 
}
