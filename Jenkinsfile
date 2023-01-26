pipeline {
    agent { docker { image 'node:6.3' } }
    stages {
        stage('Node') {
            steps {
                sh 'npm install'
            }
        }
    }
}