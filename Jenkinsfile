pipeline {
    agent { label 'Nodejs' }
    environment { 
        PROJECT = 'expense'
        COMPONENT = 'backend' 
        DEPLOY_TO = "production"
        REGION = "us-east-1"
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }
    parameters{
        string(name: 'version',  description: 'Enter the application version')
    }
    stages {
        
        stage('Deploy') {
            
            steps {
                script{
                    withAWS(region: 'us-east-1', credentials: 'aws-creds') {
                        sh """
                            aws eks update-kubeconfig --region $REGION --name expense-dev
                            kubectl get nodes
                        """
                    }
                }
            }
        }
        
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure { 
            echo 'I will run when pipeline is failed'
        }
        success { 
            echo 'I will run when pipeline is success'
        }
    }
}