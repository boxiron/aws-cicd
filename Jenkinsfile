pipeline {
    agent any 

    environment {
        BRANCH_NAME = 'main'
        GIT_URL = 'https://github.com/boxiron/aws-cicd.git'
    }

    stages {
        stage('git checout'){
            steps{
                git branch: "${BRANCH_NAME}" , url: "${GIT_URL}"
            }
        }
        stage('docker build'){
            steps{
                sh 'docker build -t awscicd .'
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