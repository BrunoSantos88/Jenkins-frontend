pipeline {

agent { docker 'maven:3.8.7-eclipse-temurin-11' } 
agent {
    // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
    dockerfile {
        filename 'Dockerfile.build'
        dir 'build'
        label 'my-defined-label'
        additionalBuildArgs  '--build-arg version=1.0.2'
        args '-v /tmp:/tmp'
    }
}

stages {
        stage('Example Build') {
            steps {
                sh 'mvn -B clean verify'
            }
        }

}
}