pipeline {
    agent { docker { image 'node:6.3' } }
    stages {
        stage('Node Agent') {
            steps {
                sh 'npm install'
            }
        }
    
stage ('Maven') {
   agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    
          stage ("build") {
              steps {
                sh 'mvn clean package jib:dockerBuild verify'
              }
        }
    }
}
    }
