pipeline {
    agent any

    environment {
        EC2_IP = 13.233.83.120
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/AbhishekNS2004/pipe.git'
            }
        }

        stage('Verify Files') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {

                    sh '''
                    scp -o StrictHostKeyChecking=no \
                    index.html style.css \
                    ubuntu@$EC2_IP:/tmp/
                    '''

                    sh '''
                    ssh -o StrictHostKeyChecking=no \
                    ubuntu@$EC2_IP "
                    sudo cp /tmp/index.html /var/www/html/
                    sudo cp /tmp/style.css /var/www/html/
                    "
                    '''
                }
            }
        }
    }
}
