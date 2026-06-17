pipeline {
    agent any

    environment {
        EC2_IP = "13.233.83.120"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/AbhishekNS2004/pipe.git'
            }
        }

        stage('Deploy Website') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                    scp -o StrictHostKeyChecking=no index.html ubuntu@$EC2_IP:/tmp/

                    ssh -o StrictHostKeyChecking=no ubuntu@$EC2_IP "
                    sudo cp /tmp/index.html /var/www/html/index.html
                    "
                    '''
                }
            }
        }
    }
}
