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
        stage ('Pushing the docker image to docker repository'){
          steps{
            script{
                docker.withRegistry('https://registry.hub.docker.com', 'docker-credentials') {
                docker.push ('latest')
                docker.push ('$BUILD_NUMBER')
                }
             }
          }

        }
    }
}
