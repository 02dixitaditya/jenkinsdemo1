// pipeline {
//   agent any 
  
//   stages {
  
//     stage('Build') {
//        steps {
//           echo 'build'
//           sh 'javac myfile.java'
//         }
//     }
    
//     stage('Test') {
//        steps {
//           echo 'testing' 
//           sh 'java myfile'
//        }
//     }

//     stage('Dockerfile'){
//       steps {
//         sh 'docker volume create hostfolder'
//         sh 'docker build -t demodoc --build-arg TEST=150 .'
//         //sh 'docker run -it -v hostfolder:/dockerfolder --name demodoc'
//         sh 'docker run -it -v hostfolder:/dockerfolder -d demodoc:latest'
      
//       }
//     }
    
//  }
// }










node {
  
  try{
      stage('Build'){
        echo 'build'
	sleep(time:10,unit:"SECONDS")
        //sh 'javac myfile.java'
      }
      stage('Test') {
           echo 'testing' 
	   sleep(time:10,unit:"SECONDS")
           //sh 'java myfile'
        }

        stage('Dockerfile'){
            //sh 'docker volume create hostfolder'
	    sh 'docker build -t mydoc --build-arg TEST=150 .'
            sleep(time:10,unit:"SECONDS")
	    //sh 'docker run -it -v hostfolder:/dockerfolder --name demodoc'
	    //sh 'docker run -it -v hostfolder:/dockerfolder -d demodoc:latest'
        }
  }
  catch (Exception ex) {
            echo 'error'
        } 
  finally {
            echo 'finally'
            //cleanWs()
            sh('docker system prune -a -f --volumes')
	}
  
}
