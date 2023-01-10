pipeline {
    agent any
    tools {
       terraform 'Terraform 1.3.7'
    }

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

        stages {
        
    stage('Clone repository') { 
      steps { 
        script{
          checkout scm
            }
             } 
    }

        stage('Terraform Init') {
            steps {
                sh 'terraform init '
                
            }
        }

        stage('Apply') {
            steps {
          sh 'terraform apply -auto-approve'
            }
        }
    }
}