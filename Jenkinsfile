pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
    IP_DE_NEXUS = 127.0.0.1
  }
   stages {
     stage('Building image') {
        steps{
            sh '''
            docker build -t sumador .
               '''  
          }
      }
    
    
      stage('Run tests') {
        steps {
          sh "docker run sumador npm test"
        }
      }
      stage('Deploy Image') {
        steps {
          withCredentials([usernamePassword(credentialsId: 'f0142294-69d8-4e13-9215-33104e705eb6', usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
              script {
                  sh "docker login -u $NEXUS_USERNAME -p $NEXUS_PASSWORD your-docker-registry-url"
                  sh '''
                  docker tag sumador 127.0.0.1:8083/mundose/sumador
                  docker push 127.0.0.1:8083/mundose/sumador   
                  '''
              }
          }
        }
      }
    }
}


    
  

