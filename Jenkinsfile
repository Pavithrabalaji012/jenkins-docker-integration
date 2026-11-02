pipeline {
    agent any
  environment {
    IMAGE_NAME = 'jenkins-docker-practice:latest'
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
                sh 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Show Docker Images') {
      steps {
        bat "docker images"
      }
    }
    }
}
