pipeline {
  agent any
  stages {
    stage("Build") {
    docker.image('maven:3.6.1-jdk-11-slim').inside('-v $HOME:/var/maven -e MAVEN_CONFIG=/var/maven/.m2'){
        sh "mvn clean package"
    }
    }
  }
}