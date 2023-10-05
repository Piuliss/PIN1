pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
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
        steps{
          sh '''
          docker tag sumador 127.0.0.1:5000/mguazzardo/sumador
          docker push 127.0.0.1:5000/mguazzardo/sumador   
          '''
          }
      }
    }
}


    
  

