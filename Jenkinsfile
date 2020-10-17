pipeline{
    environment {
        registry = "shahid9741/jenkins"
        registryCredential = 'docker-credentials'
        docker = ''
    }
    agent any
    stages{
        stage ('Checkout code'){
          steps{
                checkout scm              
          }
        }
        stage ('Building jenkins image'){
          steps{
            script{
            docker = docker.build registry + ":$BUILD_NUMBER"
            }
          }
        }
    }
}
