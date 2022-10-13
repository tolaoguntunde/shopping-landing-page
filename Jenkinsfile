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
                    ssh -i $SSH_CRED -t -o StrictHostKeyChecking=no ubuntu@ec2-35-183-122-243.ca-central-1.compute.amazonaws.com << EOF
                    sudo mkdir pearlshop
                    cd pearlshop
                    sudo git clone https://github.com/tolaoguntunde/shopping-landing-page.git .
                    cd ..
                    sudo rm -rf /var/www/pearlshop
                    sudo cp -r pearlshop /var/www/
                    echo "exiting terminal"
                    exit
                    << EOF
                    """
                }
            }
        }
    }
}
