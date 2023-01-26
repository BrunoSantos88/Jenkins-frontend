pipeline {
  agent any
}
 
   stage("install pip dependencies") {
      agent { 
        docker {
           label "docker" 
            image "python:3.7"
           }
           }
   }