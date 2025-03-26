pipeline {
    agent any
    environment {
        GIT_REPO = 'https://github.com/gagangupta023/capstone-project.git'
        AWS_SERVER = 'ubuntu@54.80.216.168'
        AZURE_SERVER = 'azureuser@52.151.248.186'
        SSH_KEY = '/var/lib/jenkins/.ssh/upgrad-key'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: "${GIT_REPO}"
            }
        }
        stage('Deploy to AWS') {
            steps {
                script {
                    sh """
                    chmod 600 ${SSH_KEY}
                    scp -o StrictHostKeyChecking=no -i ${SSH_KEY} index-aws.html ${AWS_SERVER}:/home/ubuntu/index.html
                    ssh -o StrictHostKeyChecking=no -i ${SSH_KEY} ${AWS_SERVER} 'sudo mv /home/ubuntu/index.html /var/www/html/index.html && sudo systemctl restart nginx'
                    """
                }
            }
        }
        stage('Deploy to Azure') {
            steps {
                script {
                    sh """
                    chmod 600 ${SSH_KEY}
                    scp -o StrictHostKeyChecking=no -i ${SSH_KEY} index-azure.html ${AZURE_SERVER}:/home/azureuser/index.html
                    ssh -o StrictHostKeyChecking=no -i ${SSH_KEY} ${AZURE_SERVER} 'sudo mv /home/azureuser/index.html /var/www/html/index.html && sudo systemctl restart nginx'
                    """
                }
            }
        }
    }
