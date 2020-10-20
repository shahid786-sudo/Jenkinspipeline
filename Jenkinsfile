pipeline{
    environment {
        registry = "shahid9741/jenkins"
        registryCredential = 'docker-credentials'
        dockerapp = ''
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
            dockerapp = docker.build registry + ":$BUILD_NUMBER"
            }
          }
        }
        stage ('Pushing the docker image to docker repository'){
          steps{
            script{
                docker.withRegistry( '', registryCredential ) {
		dockerapp.push('latest')
                dockerapp.push ('$BUILD_NUMBER')
                }
             }
          }

        }
        stage ('Deployment of jenkins application on node01'){
        steps{
          script{
            sh 'echo "Deploying jenkins application"'
            sh '''
            kubectl create -f Jenkinsdeployment.yaml
            '''        
          }
        }
    }
 }
}
