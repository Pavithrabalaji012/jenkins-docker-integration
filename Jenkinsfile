pipeline {
    agent any
  environment {
    IMAGE_NAME = 'jenkins-docker-practice:latest'
      DOCKERHUB_CREDENTIALS = 'docker-hub-token'  // your Docker Hub credentials ID in Jenkins
    DOCKERHUB_REPO = 'pavithradhrithi/jenkins-docker-integration'  // replace with your Docker Hub repo
  }

    stages {

        stage('Checkout') {
            steps {
                echo 'Getting code from GitHub'
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Show Docker Images') {
      steps {
        bat "docker images"
      }
    }

    stage('Docker Login and Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: DOCKERHUB_CREDENTIALS, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          bat """
            docker login -u %DOCKER_USER% -p %DOCKER_PASS%
            docker tag %IMAGE_NAME% %DOCKERHUB_REPO%:latest1
            docker push %DOCKERHUB_REPO%:latest1
          """
        }
      }
    }
        stage('Pull Docker Image') {
      steps {
        bat "docker pull %DOCKERHUB_REPO%:latest1"
      }
    }

    stage('Deploy Docker Container') {
      steps {
        bat 'docker run -d -p 80:3000 --name jen-doc-container %DOCKERHUB_REPO%:latest1'
      }
    }
}
}
