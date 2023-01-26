pipeline {
  agent none
  stages {
    stage('snyk dependency scan') {
      agent {
        docker {
          image 'snyk/snyk-cli:python-3'
        }
      }
      environment {
        SNYK_TOKEN = credentials('SNYK_TOKEN')
      }	
      steps {
        sh """
          pip install -r requirements.txt
          snyk auth ${SNYK_TOKEN}
          snyk test --json \
            --severity-threshold=high \
            --file=requirements.txt \
            --org=cloudbees \
            --project-name=project-python
        """		
      }
    }
  }
}


  