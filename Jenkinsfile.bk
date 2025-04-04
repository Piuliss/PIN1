pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
    IP_DE_NEXUS = "http://localhost"
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
              docker.withRegistry('http://localhost:8083', 'f0142294-69d8-4e13-9215-33104e705eb6') {
                def imageName = "sumador:${env.BUILD_NUMBER}"
                def dockerImage = docker.build(imageName, '.')
                dockerImage.push()
              }
            }
        }
      }
    }
  }
}


    
  

