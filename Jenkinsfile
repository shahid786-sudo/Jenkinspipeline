pipeline{
    environment {
        registry = "shahid9741/jenkins"
        registryCredential = "docker-credentials"
        dockerapp = ''
    }
    agent any
    stages {
        stage ('Checkout scm'){
            steps{
                checkout scm
            }
        }
    }
        stage('Building jenkins image'){
            steps{
            script{
                dockerapp = docker.build + "$BUILD_NUMBER"
            }
        }
    }
}