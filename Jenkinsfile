pipeline {
    agent any

    options {
        timeout(time: 2, unit: 'MINUTES') // Tiempo máximo para la ejecución del pipeline
    }

    environment {
        IMAGE_NAME = "sumador" // Nombre de la imagen Docker
        IMAGE_TAG = "${env.BUILD_NUMBER}" // Etiqueta de la imagen basada en el número de build
        NEXUS_REPO_URL = "http://localhost:8081/repository/MyRepoJenk/" // URL del repositorio Nexus
        ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh """
                docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                """
            }
        }

        stage('Run tests') {
          steps {
            sh "docker run ${IMAGE_NAME}:${IMAGE_TAG} npm test"
          }
        }
        

        stage('Tag Docker Image') {
            steps {
                echo "Tagging Docker image for Nexus repository..."
                sh """
                docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${NEXUS_REPO_URL}${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }


        stage('Push Docker Image to Nexus') {
            steps {
                echo "Pushing Docker image to Nexus repository..."
                sh """
                docker push ${NEXUS_REPO_URL}${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }
    }

    post {
        always {
            echo "Cleaning up local Docker images..."
            sh """
            docker rmi ${IMAGE_NAME}:${IMAGE_TAG} || true
            docker rmi ${NEXUS_REPO_URL}${IMAGE_NAME}:${IMAGE_TAG} || true
            """
        }
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check the logs for details."
        }
    }
}