pipeline {
  agent any
  
  tools { 
        ///depentencias 
        maven 'Maven 3.5.2' 
    }


   stage("install pip dependencies") {
      agent { 
        docker {
           label "docker" 
            image "python:3.7"
           }
           }
   }


stage('Clone repository') { 
steps { 
script{
checkout scm
}
}
}

}