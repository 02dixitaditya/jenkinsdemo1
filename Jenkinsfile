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
}}

}
}
