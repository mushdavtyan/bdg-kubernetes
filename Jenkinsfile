pipeline {
     agent any
        environment {
        registry = "amazon/registry"
        registryCredential = 'AWS-ECR'
        dockerImage = ''
    }
    stages {

        stage ('checkout') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/something.git']]])
            }
        }
       
        stage ('Build docker image') {
            steps {
                script {
                dockerImage = docker.build registry
                }
            }
        }
       
         // Uploading Docker images into Docker Hub
         
    stage('Deploy image') {
        steps{
            script{
                docker.withRegistry("https://" + registry, registryCredential) {
                    dockerImage.push()
                }
            }
        }
    }
  
    }  
}
