pipeline {
    agent any 

    environment {
        BRANCH_NAME = 'main'
        GIT_URL = 'https://github.com/boxiron/aws-cicd.git'
        IMAGE_TAG = 'boxiron/aws-cicd'
        IMAGE_VERSION = $"{BUILD_NUMBER}"
    }

    stages {
        stage('git checout'){
            steps{
                git branch: "${BRANCH_NAME}" , url: "${GIT_URL}"
            }
        }
        stage('docker build'){
            steps{
                sh 'docker build -t "${IMAGE_TAG}:${IMAGE_VERSION}" .'
                sh 'docker images'
            }
        }
        stage('god is good'){
            steps{
                sh 'echo god is good'
            }
        }
    }
}