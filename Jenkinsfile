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
                    ssh -i $SSH_CRED -t -o StrictHostKeyChecking=no ubuntu@15.223.5.96 << EOF
                    sudo mkdir pearlshop.com
                    cd pearlshop.com
                    sudo git clone https://github.com/tolaoguntunde/shopping-landing-page.git .
                    cd ..
                    sudo cp -r pearlshop.com /var/www/
                    echo "exiting terminal"
                    exit
                    << EOF
                    """
                }
            }
        }
    }
}
