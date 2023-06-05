pipeline {
    agent any
    
    stages {
        stage('deploy') {
            steps {
                sh label: 'Deploy dv-bundle', script: '''
                  #!/bin/bash +x
                  
                  NODE_PRIVATE_IP=$(echo $JUMPHOST_PRIVATE_IP | awk -F. '{print $1"."$2"."$3"."$4+1}')
                  LOAD_BALANCE_IPRANGE=$(echo $JUMPHOST_PRIVATE_IP | awk -F. '{print $1"."$2"."$3".150-"$1"."$2"."$3".160"}')
                  
                  echo '{
                      "nodes":[
                        {
                          "type":"controlplane",
                          "address":"'$NODE_PRIVATE_IP'",
                          "hostname":"node1"
                        },
                    ' > file.json
                    for ((i=2;i<=NODES_COUNT;i++))
                    do
                      NODE_PRIVATE_IP=$(echo $NODE_PRIVATE_IP | awk -F. '{print $1"."$2"."$3"."$4+1}')
                      if [ $i -eq $NODES_COUNT ]
                      then 
                          echo '    {
                              "type":"worker",
                              "address":"'$NODE_PRIVATE_IP'",
                              "hostname":"node'$i'"
                            }' >> file.json
                      else 
                          echo '    {
                              "type":"worker",
                              "address":"'$NODE_PRIVATE_IP'",
                              "hostname":"node'$i'"
                            },' >> file.json
                      fi
                    done
                    echo '  ],
                      "load-balancer-ipranges": "'$LOAD_BALANCE_IPRANGE'",
                      "network-interface-name": "eth0"
                    }' >> file.json
                    
                    
                    echo "export JUMPHOST_IP=$JUMPHOST_PUBLIC_IP" > $WORKSPACE/node_creds
                    echo 'export SSH_USERNAME="root"' >> $WORKSPACE/node_creds
                    echo 'export SSH_PASSWORD="rain"' >> $WORKSPACE/node_creds

                    source $WORKSPACE/node_creds
                    sshpass -p $SSH_PASSWORD scp -o StrictHostKeyChecking=no $WORKSPACE/file.json $SSH_USERNAME@$JUMPHOST_IP:~
                    DEPLOYER_USERNAME=administrator@kalyani.local
                    DEPLOYER_PASSWORD=P@ssw0rd
                    curl -u $DEPLOYER_USERNAME:$DEPLOYER_PASSWORD https://amaas-eos-mw1.cec.lab.emc.com/artifactory/dv-installer/weekly/1.0.0.0-18-193-200785a
                '''
            }
        }
    }
}

