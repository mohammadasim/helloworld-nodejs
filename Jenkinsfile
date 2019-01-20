pipeline{
    agent any
    environment {
        SERVER_PRIVATE_IP='10.0.5.205'
    }
    tools {
        nodejs "nodejs"
    }
    stages {
        stage('Clone app repo'){
            steps {
                url: git 'https://github.com/mohammadasim/helloworld-nodejs.git'
            }
        }
        stage('Build'){
            steps{
                sh ''' #!/bin/bash
                npm install
                '''
            }
        }
        stage('Deploy'){
            steps{
                ansiblePlaybook(
                    colorized: true,
                    playbook: '$WORKSPACE/deploy/production_deploy.yml',
                    credentialsId: '025419c4-ead0-4fac-a24d-d09c27662e9f',
                    inventoryContent: '$SERVER_PRIVATE_IP',
                    disableHostKeyChecking: true,
                    extraVars: [
                        file_path: "/var/lib/jenkins/workspace/dog-nodejs"
                        ])
            }
        }
    }
}