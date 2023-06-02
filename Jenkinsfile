#!/usr/bin/env groovy

void runBuild() {
    node('master') {
        try {

            stage('Deploy dv_bundle') {
               sh label: 'Deploy dv-bundle', script: '''
                  #!/bin/bash +x
                  echo $JUMPHOST_IP
                  echo $NODES_COUNT
                  echo $DV_REPOSITORY_PATH
                '''
            }

        } catch (Exception ex) {
            echo "error"
        }
    }
}

if (env.LOAD_JENKINSFILE_AS_LIB) {
    return this
} else {
    properties([
            parameters([
                    string(
                            name: 'JUMPHOST_IP',
                            defaultValue: '',
                            description: 'Enter cluster <b>Jumphost IP</b>',
                            trim: true,
                    ),
                    string(
                            name: 'NODES_COUNT',
                            defaultValue: '',
                            description: 'Enter number of hosts',
                            trim: true,
                    ),
                    string(
                            name: 'DV_REPOSITORY_PATH',
                            defaultValue: '',
                            description: 'Enter repository path of DV bundle to be installed',
                            trim: true,
                    ),
            ]),
    ])

    this.runBuild()
}
