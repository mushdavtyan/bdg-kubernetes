pipeline {
    agent any
    environment{
        registry = "252990216717.dkr.ecr.us-east-2.amazonaws.com/bdgdevops"
        registryCredential = 'AWS-ECR'
        dockerImage = ''
    }
    stages{
        stage ('checkout')
        steps {
             checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mushdavtyan/bdg-kubernetes.git']]])            }
    }
        }
        stage ('Build docker image') {
            steps {
                script {
                dockerImage = docker.build registry
                }
            }
        }
       
         // Uploading Docker images into ECR
         
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
}
