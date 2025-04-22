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
                    // Check if Docker is already installed
                    def dockerInstalled = sh(script: 'which docker', returnStatus: true)
                    if (dockerInstalled != 0) {
                        echo 'Docker not found. Installing Docker...'
                        
                        // Disable TTY requirement for sudo by passing the argument '-S' to avoid password prompt
                        sh 'echo "jenkins ALL=(ALL) NOPASSWD: ALL" | sudo tee -a /etc/sudoers' // Optional: only for installations
                        
                        // Install Docker
                        sh 'sudo yum update -y'
                        sh 'sudo yum install -y docker'
                        sh 'sudo systemctl start docker'
                        sh 'sudo systemctl enable docker'
                        sh 'sudo usermod -aG docker ec2-user'
                        
                        echo 'Docker installed and started successfully.'
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
