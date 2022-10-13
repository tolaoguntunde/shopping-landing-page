pipeline {
  agent any
  
  stages {
        stage('test') {
            steps {
            sh "echo The login user is ${USER}"
            sh "echo Welcome to pearlshop website"
            }
        }
     

        stage('deployment') {
            environment { 
                SSH_CRED = credentials('jenkinstest-pem')
            }
            steps{         
                script {
                    sh """
                    #!/bin/bash
		            echo "connecting to remote or deploy server"	
                    ssh -i $SSH_CRED -t -o StrictHostKeyChecking=no ubuntu@3.96.195.60 << EOF
                    sudo mkdir html
                    cd html
                    sudo git clone https://github.com/tolaoguntunde/shopping-landing-page.git .
                    cd ..
                    sudo rm -rf /var/www/html
                    sudo cp -r html /var/www/
                    echo "exiting terminal"
                    exit
                    << EOF
                    """
                }
            }
        }
    }
}
