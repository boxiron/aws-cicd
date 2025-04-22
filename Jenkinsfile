pipeline {
    agent any

    environment {
        BRANCH_NAME = 'main'
        GIT_URL = 'https://github.com/boxiron/aws-cicd.git'
        IMAGE_TAG = 'boxiron/aws-cicd'
        IMAGE_VERSION = "${BUILD_NUMBER}"
    }

    stages {
        stage('Install Docker') {
            steps {
                script {
                    // Install Docker if it's not already installed
                    def dockerInstalled = sh(script: 'which docker', returnStatus: true)
                    if (dockerInstalled != 0) {
                        echo 'Docker not found. Installing Docker...'
                        sh 'sudo yum update -y'
                        sh 'sudo yum install -y docker'
                        sh 'sudo systemctl start docker'
                        sh 'sudo systemctl enable docker'
                        sh 'sudo usermod -aG docker ec2-user'
                    } else {
                        echo 'Docker is already installed.'
                    }
                }
            }
        }
        stage('Git Checkout') {
            steps {
                git branch: "${BRANCH_NAME}", url: "${GIT_URL}"
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t "${IMAGE_TAG}:${IMAGE_VERSION}" .'
                sh 'docker images'
            }
        }
        stage('God is Good') {
            steps {
                sh 'echo god is good'
            }
        }
    }
}
