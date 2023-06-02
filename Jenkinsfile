pipeline {
    agent any
    
    stages {
        stage('deploy') {
            steps {
                sh label: 'Deploy dv-bundle', script: '''
                  #!/bin/bash +x
                  echo $JUMPHOST_IP
                  echo $NODES_COUNT
                  echo $DV_REPOSITORY_PATH
                  ip=$JUMPHOST_IP
                  for ((i=1;i<=$NODES_COUNT;i++))
                  do 
                     echo $ip >> ip.txt
                     ip=$(echo $ip | awk -F. '{print $1"."$2"."$3"."$4+1}')
                  done
                '''
            }
        }
    }
}

