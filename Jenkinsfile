pipeline{
    environment {
        registry = "shahid9741/jenkins"
        registrCredential = 'docker-credentials'
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
            docker = docker.build registery + ":$BUILD_NUMBER"
            }
          }
        }
    }
}
