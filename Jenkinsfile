pipeline {
    environment {
        registry = "caotvo/squid-docker"
        registryCredential = 'dockerhub_id'
    }
    agent { label 'docker-in' }
    stages {
      stage('build images') {
        steps {
          script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER" 
          }
        }
      }
      stage('push image'){
        steps {
          script {
            docker.withRegistry( '', registryCredential ) {
              dockerImage.push() 
            }
          }
        }
      }
      stage('Clean up') {
        steps {
          sh "docker rmi $registry:$BUILD_NUMBER" 
        }
      }
    }
    
}
