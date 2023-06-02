pipeline {
    agent any
    
    stages {
        stage('deploy') {
            steps {
                sh label: 'Deploy dv-bundle', script: '''
                  #!/bin/bash +x
                  JUMPHOST_IP=$JUMPHOST_IP
                  NODES_COUNT=$NODES_COUNT
                  DV_REPOSITORY_PATH=$DV_REPOSITORY_PATH
                  PRIVATE_IP="192.168.228.100"
                  #ip a show
                  for ((i=1;i<=NODES_COUNT;i++))
                  do 
                     ip=$(echo $ip | awk -F. '{print $1"."$2"."$3"."$4+1}')
                     echo $ip >> ip.txt
                  done
                '''
            }
        }
    }
}

