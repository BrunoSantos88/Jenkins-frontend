pipeline externa {
    agent { docker { image 'maven:3.8.7-eclipse-temurin-11' } }

    stages {
        stage('Maven') {
            steps {
                sh 'mvn --version'
            }
        }
}

}
  
