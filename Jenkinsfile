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
                  JP_PRIVATE_IP="192.168.222.100"
                  NODE_PRIVATE_IP=$JP_PRIVATE_IP
                  #ip a show
                  for ((i=1;i<=NODES_COUNT;i++))
                  do 
                     NODE_PRIVATE_IP=$(echo $NODE_PRIVATE_IP | awk -F. '{print $1"."$2"."$3"."$4+1}')
                     echo $NODE_PRIVATE_IP >> ip.txt
                  done
                '''
            }
        }
    }
}

