pipeline{
    agent any

    environment {
        REMOTE_USER = 'ubuntu'
        REMOTE_IP = '3.6.185.169'
        DIR = '/home/ubuntu/test'
        SSH_CRED = 'deploy-ssh-key'
    }
    stages{
        stage("Create a Directory"){
            steps{
                echo "Creating Directory ${DIR} on ${REMOTE_IP}"
                // use sshagent to provide private key
                sshagent (credentials:[SSH_CRED]){
                    sh """
                        ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_IP} 'mkdir -p ${DIR} && ls -ld ${DIR}'
                    """
                }
            }

        }
    }
    post{

        success{
            echo "Done: directory created (if SSH connection succeeded)"
        }
        failure{
            echo "Failed — check console output for SSH errors"
        }
    }
}