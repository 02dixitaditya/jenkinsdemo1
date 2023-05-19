pipeline {
  agent any 
  
  stages {
  
    stage('Build') {
       steps {
          echo 'build'
          sh 'javac myfile.java'
        }
    }
    
    stage('Test') {
       steps {
          echo 'testing' 
          sh 'java myfile'
       }
    }

    stage('Dockerfile'){
      steps {
        sh 'docker volume create hostfolder'
        sh 'docker build -t demodoc --build-arg TEST=150 .'
        //sh 'docker run -it -v hostfolder:/dockerfolder --name demodoc'
        sh 'docker run -it --name demodoc:latest'
      
      }
    }
    
 }
}
