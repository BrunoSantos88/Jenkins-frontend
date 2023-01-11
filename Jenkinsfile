pipeline {
  agent any
  tools { 
        maven 'Maven 3.6.3'  
    }

    environment {
    registry = "brunosantos88/awsfrontend"
    registryCredential = 'dockerlogin'
    dockerImage = ''
  }


  stages{

    stage('Clone repository') { 
steps { 
script{
checkout scm
}
}
}
    stage('Synk-GateSonar-Security') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
  }

      stage('Kubernetes Apply') {
          steps {
          sh 'terraform apply -auto-approve'
          sh 'terraform output kubeconfig > ./kubeconfig'
          sh 'terraform output config_map_aws_auth > ./config_map_aws_auth.yaml'
          sh 'export KUBECONFIG=./kubeconfig'
            }
        }
        }
  }

   
