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
                '''
            }
        }
    }
}

