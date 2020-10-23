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
          sshagent(['kube-master-node']){
          sh 'ssh -vvv -o StrictHostKeyChecking=no -T shahid@192.168.0.8'
          sh 'scp -r Jenkinsdeployment.yaml shahid@192.168.0.8:/home/shahid'
          sh 'ssh shahid@192.168.0.8 kubectl create -f Jenkinsdeployment.yaml'
             }
          }
        }
    }
}

